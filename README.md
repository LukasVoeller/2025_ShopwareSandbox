# Shopware 6 Sandbox

Diese Sandbox dient als lokale Entwicklungsumgebung fuer Shopware-6-Projekte auf Basis von [Lando](https://lando.dev/).

## Zweck

Das Projekt stellt eine lauffaehige Shopware-6-Installation fuer die lokale Entwicklung bereit. Der Fokus liegt auf:

- Entwicklung von Shopware-Plugins und individuellen Erweiterungen
- Build- und Watch-Workflows fuer Administration und Storefront
- lokaler Ausfuehrung von Qualitaetssicherung mit Composer, PHPStan und ECS

## Technischer Stack

- Shopware 6.5
- PHP 8.2
- Apache 2.4
- MySQL 8.0
- Redis 7
- MailHog
- Node.js 18
- Lando als lokale Orchestrierung

## Projektstruktur

- `custom/plugins/*`: lokale Shopware-Plugins als Composer-Pfad-Repositories
- `custom/plugins/*/packages/*`: zusaetzliche Paketquellen innerhalb von Plugins
- `custom/static-plugins/*`: weitere lokale statische Plugins
- `bin/`: Build-, Watch- und Konsolen-Skripte
- `config/`: Symfony- und Shopware-Konfiguration
- `tests/`: Test-Bootstrap

## Voraussetzungen

Vor der Nutzung sollten lokal installiert sein:

- Docker bzw. Docker Desktop
- Lando

## Umgebung starten

Die Entwicklungsumgebung wird mit Lando gestartet:

```bash
lando start
```

Danach stehen die konfigurierten Services wie Appserver, Datenbank, Redis und MailHog zur Verfuegung.

## Wichtige Befehle

### Shopware-Konsole

```bash
lando console
```

Beispiel:

```bash
lando console cache:clear
```

### Composer

```bash
lando composer install
```

Weitere Composer-Befehle lassen sich ueber dasselbe Tooling ausfuehren.

### Codequalitaet

PHPStan ausfuehren:

```bash
lando phpstan
```

Easy Coding Standard ausfuehren:

```bash
lando ecs
```

Prettier ausfuehren:

```bash
lando prettier
```

## Frontend-Builds

Build fuer Administration und Storefront:

```bash
lando build-js
```

Nur Storefront bauen:

```bash
lando build-storefront
```

Nur Administration bauen:

```bash
lando build-administration
```

## Watcher fuer die Entwicklung

Storefront-Watcher starten:

```bash
lando watch-storefront
```

Administration-Watcher starten:

```bash
lando watch-administration
```

## Debugging

Xdebug kann bei Bedarf ueber Lando aktiviert oder deaktiviert werden:

```bash
lando xdebug-on
lando xdebug-off
```

## Hinweise

- Die PHP-Konfiguration wird ueber `.lando/php/php.ini` eingebunden.
- Die lokale `.env` wird beim Start aus `.lando/.lando.env` verlinkt.
- Mailversand laeuft ueber MailHog.
- Lokale Plugins werden als Pfad-Repositories eingebunden und koennen direkt in dieser Sandbox entwickelt werden.
