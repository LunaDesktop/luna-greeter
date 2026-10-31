# Luna Greeter

Login screen for the Luna desktop — a greetd frontend built on libLuna.

> **Languages:** [Polski](README.pl.md) · [English](README.en.md) · [Deutsch](README.de.md)

## Part of the Luna project

The greeter is UI-only: PAM, logind and session startup stay inside `greetd`.
It runs as the unprivileged `greeter` user and talks to the daemon over a Unix
socket. It supports local accounts, Wayland/X11 sessions, AccountsService
avatars and appearance settings stored in `/etc/luna/greeter.conf`.

## Building

```sh
cargo build --release --locked
cargo run -- --preview
```

License: GPL-3.0-or-later. Details: [`docs/greeter.md`](docs/greeter.md).
