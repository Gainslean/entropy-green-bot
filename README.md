# Entropy GREEN — spread bot for Hyperliquid HIP-3 (compiled)

**🌐 Сайт / Website: [https://entropybot.app](https://entropybot.app)** · [Русский](#русский) · [English](#english)

> **Сайт:** https://entropybot.app — инструкции, статистика, скачивание.
> **Website:** https://entropybot.app — guides, statistics, downloads.

**Версия 1.2.1 / Version 1.2.1**

## Русский

**1.2.1:** выход в профит: срок отправки считается от времени стакана на бирже, устаревший стакан не даёт отправить заявку на выход; повтор частичного выхода сверяет остаток ног по свежему снимку позиций, после последней попытки сразу начинается аварийное закрытие; в новых установках фильтр медленного дрейфа базиса закрывает входы только на SNDK (на остальных рынках считает и пишет в журнал). Торговые пороги и размеры не менялись; контракт выхода открытых позиций тот же.

Торговый бот для спреда между двумя биржами HIP-3 на Hyperliquid — **Entropy (io)** и **TRADE.XYZ (xyz)** — на рынках NBIS, DRAM, EWY, SNDK.
Режим **GREEN**: позиция закрывается в плюс; с 7-го часа удержания бот согласен выйти в ноль, а через 10 часов закрывает позицию.

Программа поставляется **в скомпилированном виде** (без исходного кода), ставится одной командой, сама настраивается и **сама проверяет обновления раз в час** — в панели появляется баннер «Доступно обновление» и кнопка «Обновить».

### Что нужно
- Linux-сервер: Ubuntu 22.04 / 24.04 или Debian 12, x86-64, 2 ядра, 2–4 ГБ памяти, 10 ГБ диска (лучше в Токио).
- От 1 до 9 кошельков Hyperliquid с USDC (рекомендуется от ~$100–150 на кошелёк).
- Каждый кошелёк должен быть зарегистрирован по реферальным ссылкам — **иначе бот не будет на нём торговать** (проверка встроена и не отключается):
  - Hyperliquid / TRADE.XYZ: https://app.hyperliquid.xyz/join/CRYPTOGAINS
  - Entropy: https://entropy.io/?r=cryptogains

### Скачать
- Последняя версия всегда здесь: **[Releases](../../releases/latest)** — файл `entropy-green-<версия>.tar.gz`
- Или с сервера загрузок (всегда последняя): http://168.144.242.18:8080/get/entropy-green-latest.tar.gz
- Контрольные суммы: `SHA256SUMS` в релизе и на http://168.144.242.18:8080/get/SHA256SUMS

### Установка (на сервере)
```bash
cd ~ && curl -fL -o entropy-green-latest.tar.gz http://168.144.242.18:8080/get/entropy-green-latest.tar.gz
sha256sum entropy-green-latest.tar.gz   # сверьте с SHA256SUMS
rm -rf entropy-green && mkdir entropy-green && tar xzf entropy-green-latest.tar.gz -C entropy-green --strip-components=1
sudo bash entropy-green/install-green.sh
```
Установщик спросит только кошельки (ключ вводится скрыто и хранится только на вашем сервере), всё остальное сделает сам и в конце напечатает ссылку на панель `https://IP_СЕРВЕРА:8443`, логин и пароль. Торговля включается отдельной командой `sudo bash /opt/entropy-green/install-green.sh --live`.

Подробная инструкция — [INSTALL.md](INSTALL.md).

### Обновление
Кнопка «Обновить» в панели (бот сам проверяет обновления раз в час и показывает баннер), или:
```bash
sudo bash /opt/entropy-green/install-green.sh --update-now
```

> Торговля связана с риском потерь. Используйте только средства, которые готовы потерять. Ключи агента (API wallet) никогда не покидают ваш сервер; seed-фразу кошелька боту не вводите.

## English

**1.2.1:** profit exits: the send deadline is measured from the exchange order-book time, so a stale book no longer sends an exit order; the partial-exit retry reconciles the remaining legs from a fresh position snapshot and goes straight to the emergency close after the last attempt; on new installs the slow basis-drift filter blocks entries only on SNDK (it still computes and logs on the other markets). Trading thresholds and sizes are unchanged; the exit contract of open positions is the same.

A spread-trading bot between two Hyperliquid HIP-3 venues — **Entropy (io)** and **TRADE.XYZ (xyz)** — on NBIS, DRAM, EWY and SNDK.
**GREEN** mode: positions close in profit; from hour 7 the bot accepts a break-even exit, and closes the position at 10 hours.

Shipped **compiled** (no source code), installs with one command, configures itself and **checks for updates every hour** (a banner and an «Update» button appear in the dashboard).

### Requirements
- Linux server: Ubuntu 22.04 / 24.04 or Debian 12, x86-64, 2 vCPU, 2–4 GB RAM, 10 GB disk (Tokyo is best).
- 1–9 Hyperliquid wallets funded with USDC (~$100–150+ each recommended).
- Every wallet must be registered through these referral links — **otherwise the bot will not trade it** (built-in, cannot be disabled):
  - Hyperliquid / TRADE.XYZ: https://app.hyperliquid.xyz/join/CRYPTOGAINS
  - Entropy: https://entropy.io/?r=cryptogains

### Download
- Latest release: **[Releases](../../releases/latest)** — `entropy-green-<version>.tar.gz`
- Or always-latest link: http://168.144.242.18:8080/get/entropy-green-latest.tar.gz (checksums: `SHA256SUMS`)

### Install
```bash
cd ~ && curl -fL -o entropy-green-latest.tar.gz http://168.144.242.18:8080/get/entropy-green-latest.tar.gz
sha256sum entropy-green-latest.tar.gz   # compare with SHA256SUMS
rm -rf entropy-green && mkdir entropy-green && tar xzf entropy-green-latest.tar.gz -C entropy-green --strip-components=1
sudo bash entropy-green/install-green.sh
```
The installer asks only for the wallets, does everything else, and prints the dashboard link `https://SERVER_IP:8443` with login and password. Live trading is enabled separately: `sudo bash /opt/entropy-green/install-green.sh --live`.

Full guide (Russian): [INSTALL.md](INSTALL.md).

### Update
The «Update» button in the dashboard, or `sudo bash /opt/entropy-green/install-green.sh --update-now`.

> Trading carries risk of loss. Agent (API wallet) keys never leave your server; never enter your wallet seed phrase.
