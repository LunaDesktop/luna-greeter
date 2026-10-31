# Luna Greeter

Anmeldebildschirm für Luna — ein greetd-Frontend auf Basis von libLuna.

> **Sprachen:** [Polski](README.pl.md) · [English](README.en.md) · [Deutsch](README.de.md)

## Teil des Luna-Projekts

Der Greeter ist reine UI: PAM, logind und Sitzungsstart bleiben in `greetd`.
Er läuft als unprivilegierter Benutzer `greeter` und kommuniziert über einen
Unix-Socket mit dem Daemon. Unterstützt lokale Konten, Wayland/X11-Sitzungen,
AccountsService-Avatare und Darstellungseinstellungen in `/etc/luna/greeter.conf`.

## Bauen

```sh
cargo build --release --locked
cargo run -- --preview
```

Lizenz: GPL-3.0-or-later. Details: [`docs/greeter.md`](docs/greeter.md).
