# Luna Greeter

Ekran logowania dla Luny — frontend greetd zbudowany na libLunie.

> **Języki:** [Polski](README.pl.md) · [English](README.en.md) · [Deutsch](README.de.md)

## Część projektu Luna

Greeter odpowiada tylko za interfejs: PAM, logind i start sesji wykonuje
`greetd`. UI działa jako użytkownik `greeter` i łączy się z daemonem przez
gniazdo Unix. Obsługuje konta lokalne, sesje Wayland/X11, awatary
AccountsService oraz konfigurację wyglądu zapisywaną w `/etc/luna/greeter.conf`.

## Budowanie

```sh
cargo build --release --locked
cargo run -- --preview
```

Licencja: GPL-3.0-or-later. Szczegóły: [`docs/greeter.md`](docs/greeter.md).
