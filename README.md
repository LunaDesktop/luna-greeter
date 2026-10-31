# Luna Greeter (`luna-greeter`)

> [Polski](README.pl.md) · [English](README.en.md) · [Deutsch](README.de.md)

Ekran logowania środowiska Luna, zbudowany na libLunie. Greeter jest wyłącznie
frontendem [greetd](https://git.sr.ht/~kennylevinsen/greetd): PAM, logind i
uruchomienie sesji zostają po stronie daemona, a UI działa jako nieuprzywilejowany
użytkownik `greeter`.

```sh
cargo build --release --locked
cargo test --lib
cargo run -- --preview          # podgląd bez gniazda greetd
cargo run --bin luna-greeter-config -- --help
```

## Funkcje

- **Protokół greetd** — `create_session`, `auth_message` (`visible` / `secret` /
  `info` / `error`), `post_auth_message_response`, `success`, `start_session`;
  komunikacja przez gniazdo Unix (`GREETD_SOCK`, zwykle `/run/greetd-ipc`).
- **Konta** — lista lokalnych użytkowników z `/etc/passwd` (UID 1000–69999),
  dowolna nazwa wpisana ręcznie (LDAP/SSSD), awatary z AccountsService.
- **Sesje** — wykrywanie wpisów Wayland/X11 z systemowych katalogów XDG,
  wybór sesji przed logowaniem, domyślnie sesja Luny.
- **Wygląd** — tapeta, motyw jasny/ciemny/auto, akcent i zegar ustawiane
  w *Ustawienia → Ekran logowania* (`/etc/luna/greeter.conf`).
- **Opcje systemu** — wyłączenie, restart, tryb awaryjny, konsola na `tty2`,
  Ustawienia Luny; `luna-greeter-config` zapisuje konfigurację przez `pkexec`,
  parsując wyłącznie znane klucze.
- **Zapamiętywanie** — ostatnie konto i sesja w pliku stanu `0600`, zapis atomowy;
  polecenie sesji zawsze pochodzi z systemowych plików `.desktop`, nigdy ze stanu.

## Prywatność

Greeter nie wysyła żadnych danych poza urządzenie. Czyta wyłącznie lokalne
źródła systemowe (`/etc/passwd`, AccountsService, `*.desktop`) i nie ma
komponentu sieciowego.

## Instalacja

```sh
install -Dm755 target/release/luna-greeter        /usr/bin/luna-greeter
install -Dm755 target/release/luna-greeter-config /usr/bin/luna-greeter-config
install -Dm755 session/luna-greeter-session       /usr/bin/luna-greeter-session

# Ikona ekranu logowania (motyw Luna-Icons i tapeta pochodzą z luna-branding).
install -Dm644 assets/branding/luna-greeter.svg \
    /usr/share/icons/hicolor/scalable/apps/luna-greeter.svg
for s in 16 24 32 48 64 128 256 512; do
    install -Dm644 "assets/branding/hicolor/${s}x${s}/apps/luna-greeter.png" \
        "/usr/share/icons/hicolor/${s}x${s}/apps/luna-greeter.png"
done

install -Dm644 greetd/config.toml.example         /usr/share/luna/greetd/config.toml.example
```

Konfiguracja greetd (`/etc/greetd/config.toml`):

```toml
[terminal]
vt = 1

[default_session]
command = "luna-greeter-session"
user = "greeter"
```

Konto `greeter` musi mieć dostęp do DRM/wejścia (`video`, `render`, `input`) —
w PaganOS tworzy je pakiet `greetd`. Motyw ikon i domyślną tapetę instaluje
pakiet `luna-branding`.

## Dokumentacja

Pełny opis protokołu, wykrywania sesji, awatarów i konfiguracji:
[`docs/greeter.md`](docs/greeter.md).

Licencja: GPL-3.0-or-later.
