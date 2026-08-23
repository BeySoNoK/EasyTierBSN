# EasyTier

[![Github release](https://img.shields.io/github/v/tag/EasyTier/EasyTier)](https://github.com/EasyTier/EasyTier/releases)
[![GitHub](https://img.shields.io/github/license/EasyTier/EasyTier)](https://github.com/EasyTier/EasyTier/blob/main/LICENSE)
[![GitHub last commit](https://img.shields.io/github/last-commit/EasyTier/EasyTier)](https://github.com/EasyTier/EasyTier/commits/main)
[![GitHub issues](https://img.shields.io/github/issues/EasyTier/EasyTier)](https://github.com/EasyTier/EasyTier/issues)
[![GitHub Core Actions](https://github.com/EasyTier/EasyTier/actions/workflows/core.yml/badge.svg)](https://github.com/EasyTier/EasyTier/actions/workflows/core.yml)
[![GitHub GUI Actions](https://github.com/EasyTier/EasyTier/actions/workflows/gui.yml/badge.svg)](https://github.com/EasyTier/EasyTier/actions/workflows/gui.yml)
[![GitHub Test Actions](https://github.com/EasyTier/EasyTier/actions/workflows/test.yml/badge.svg)](https://github.com/EasyTier/EasyTier/actions/workflows/test.yml)
[![Ask DeepWiki](https://deepwiki.com/badge.svg)](https://deepwiki.com/EasyTier/EasyTier)

[简体中文](/README_CN.md) | [English](/README.md) | [Русский](/README_RU.md)

> ✨ Простое, безопасное и децентрализованное решение для создания частных сетей, работающее на Rust и Tokio

<p align="center">
<img src="assets/config-page.png" width="300" alt="Страница конфигурации">
<img src="assets/running-page.png" width="300" alt="Страница работы">
</p>

📚 **[Полная документация](https://easytier.cn)** | 🖥️ **[Веб-консоль](https://easytier.cn/web)** | 📝 **[Скачать релиз](https://github.com/EasyTier/EasyTier/releases)** | 🧩 **[Сторонние инструменты](https://easytier.cn/guide/installation_gui.html#%D0%A2%D1%80%D0%B5%D1%82%D1%8C%D0%B8-%D0%B8%D0%BD%D1%81%D1%82%D1%80%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D1%8B)** | ❤️ **[Поддержать](#поддержка)**

## Возможности

### Основные возможности

- 🔒 **Децентрализация**: все узлы равны и независимы, не требуется централизованный сервер
- 🚀 **Простота использования**: поддерживается управление через веб-интерфейс, клиентское приложение и командную строку
- 🌍 **Кроссплатформенность**: работает на Win/MacOS/Linux/FreeBSD/Android и архитектурах X86/ARM/MIPS
- 🔐 **Безопасность**: шифрование AES-GCM или WireGuard для защиты от атак посредника

### Расширенные функции

- 🔌 **Эффективный NAT Traversal**: поддержка UDP и IPv6, работает даже в сетях NAT4-NAT4
- 🌐 **Прокси подсетей**: узлы могут предоставлять доступ к своим подсетям для других узлов
- 🔄 **Умная маршрутизация**: выбор маршрута с минимальной задержкой и автоматическая оптимизация
- ⚡ **Высокая производительность**: сквозная передача данных без копирования, поддержка протоколов TCP/UDP/WSS/WG

### Оптимизация сети

- 📊 **Устойчивость к потерям UDP**: прокси KCP/QUIC снижают задержку и улучшают пропускную способность в условиях потерь пакетов
- 🔧 **Веб-управление**: лёгкая настройка и мониторинг через веб-интерфейс
- 🛠️ **Zero-конфигурация**: статически скомпилированные исполняемые файлы для простого развертывания

## Быстрый старт

### 📥 Установка

Выберите способ установки, подходящий вашим потребностям:

Linux (рекомендуется):
```bash
curl -fsSL "https://github.com/EasyTier/EasyTier/blob/main/script/install.sh?raw=true" | sudo bash -s install
```
Homebrew (MacOS/Linux):

```bash
brew tap brewforge/chinese
brew install --cask easytier-gui
```
Windows (рекомендуется, запуск от имени администратора):

```powershell
irm "https://github.com/EasyTier/EasyTier/blob/main/script/install.ps1?raw=true" | iex
```
Установка через cargo (последняя разрабатываемая версия):

```bash
cargo install --git https://github.com/EasyTier/EasyTier.git easytier
```
[Скачать предварительно скомпилированные файлы ](https://github.com/EasyTier/EasyTier/releases) (рекомендуется, доступно для всех платформ)

[Установка через Docker](https://easytier.cn/guide/installation.html#%25D0%25A3%25D1%2581%25D1%2582%25D0%25B0%25D0%25BD%25D0%25BE%25D0%25B2%25D0%25BA%25D0%25B0-%25D1%2587%25D0%25B5%25D1%2580%25D0%25B5%25D0%25B7-docker)

[Установка пакета ipk для OpenWrt](https://github.com/EasyTier/luci-app-easytier)

Дополнительный шаг:

[Однокомандная регистрация в качестве системной службы](https://easytier.cn/guide/network/oneclick-install-as-service.html) (автоматический запуск в фоновом режиме при загрузке системы)

### 🚀 Основное использование
#### Быстрое построение сети с общим узлом
EasyTier поддерживает быстрое построение сети с помощью общего узла. Если у вас нет публичного IP-адреса, вы можете использовать публичный общий узел. Узлы автоматически попытаются пробить NAT и установить P2P-соединение. Если P2P не удаётся, трафик будет передаваться через общий узел.

При использовании общего узла каждый подключающийся узел должен указывать одинаковые параметры для идентификации сети `--network-name` и `--network-secret`.

Пример для двух узлов (используйте более сложные имена сети, чтобы избежать конфликтов):

На узле A выполните:

```bash
# Запуск от имени администратора
sudo easytier-core -d --network-name abc --network-secret abc -p tcp://<IP_общего_узла>:11010
```
На узле B выполните:

```bash
# Запуск от имени администратора
sudo easytier-core -d --network-name abc --network-secret abc -p tcp://<IP_общего_узла>:11010
```
После успешного запуска вы можете проверить состояние сети с помощью `easytier-cli`:

```text
| ipv4         | hostname       | cost  | lat_ms | loss_rate | rx_bytes | tx_bytes | tunnel_proto | nat_type | id         | version         |
| ------------ | -------------- | ----- | ------ | --------- | -------- | -------- | ------------ | -------- | ---------- | --------------- |
| 10.126.126.1 | abc-1          | Local | *      | *         | *        | *        | udp          | FullCone | 439804259  | 2.6.2-70e69a38~ |
| 10.126.126.2 | abc-2          | p2p   | 3.452  | 0         | 17.33 kB | 20.42 kB | udp          | FullCone | 390879727  | 2.6.2-70e69a38~ |
|              | PublicServer_a | p2p   | 27.796 | 0.000     | 50.01 kB | 67.46 kB | tcp          | Unknown  | 3771642457 | 2.6.2-70e69a38~ |
```
Вы можете проверить связность между узлами:

```bash
# Проверка связности
ping 10.126.126.1
ping 10.126.126.2
```
Примечание: если ping не проходит, возможно, брандмауэр блокирует входящий трафик. Отключите брандмауэр или добавьте разрешающие правила.

Для повышения доступности вы можете подключиться к нескольким общим узлам одновременно:

```bash
# Подключение к нескольким общим узлам
sudo easytier-core -d --network-name abc --network-secret abc -p tcp://<IP_публичного_узла>:11010 -p udp://<IP_публичного_узла>:11010
```
Децентрализованное построение сети
EasyTier по своей сути децентрализован — нет разделения на серверы и клиенты. Любое устройство может [присоединиться](https://easytier.cn/en/guide/network/oneclick-install-as-service.html) к виртуальной сети, если оно может связаться хотя бы с одним узлом в ней. Ниже показано, как настроить децентрализованную сеть:

#### Децентрализованная сеть

1. Запустите первый узел (узел A):

```bash
# Запуск первого узла
sudo easytier-core -i 10.144.144.1
```
После запуска узел будет слушать следующие порты по умолчанию:

- TCP: 11010
- UDP: 11010
- WebSocket: 11011
- WebSocket SSL: 11012
- WireGuard: 11013

2. Подключите второй узел (узел B):

```bash
# Подключение через публичный IP первого узла
sudo easytier-core -i 10.144.144.2 -p udp://<публичный_IP_первого_узла>:11010
```
Проверьте подключение:

```bash
# Проверка связности
ping 10.144.144.2

# Просмотр подключенных пиров
easytier-cli peer

# Просмотр маршрутной информации
easytier-cli route

# Просмотр информации о локальном узле
easytier-cli node
```
Чтобы добавить больше узлов, используйте параметр `-p` для подключения к любому существующему узлу в сети:

```bash
# Подключение через публичный IP любого существующего узла
sudo easytier-core -i 10.144.144.3 -p udp://<публичный_IP_любого_существующего_узла>:11010
```
### 🔍 Расширенные функции

#### Прокси подсетей

Предположим, топология сети такова, что узел B хочет предоставить другим узлам доступ к своей подсети 10.1.1.0/24:






Чтобы предоставить доступ к подсети, добавьте параметр -n при запуске EasyTier:

bash
# Предоставить доступ к подсети 10.1.1.0/24 другим узлам
sudo easytier-core -i 10.144.144.2 -n 10.1.1.0/24
Информация о прокси подсети автоматически синхронизируется со всеми узлами виртуальной сети, и на каждом узле автоматически настраиваются соответствующие маршруты. Вы можете проверить настройки прокси подсети:

Проверьте, синхронизировалась ли информация о маршрутах (в столбце proxy_cidrs отображаются проксируемые подсети):

bash
# Просмотр маршрутной информации
easytier-cli route
https:///assets/image-3.png

Проверьте доступность узлов в проксируемой подсети:

bash
# Проверка связности с проксируемой подсетью
ping 10.1.1.2
Интеграция с WireGuard
EasyTier может работать как WireGuard-сервер, позволяя любым устройствам с установленным WireGuard-клиентом (включая iOS и Android) подключаться к сети EasyTier. Пример настройки:







Запустите EasyTier с включенным порталом WireGuard:

bash
# Слушать на 0.0.0.0:11013 и использовать подсеть 10.14.14.0/24 для WireGuard-клиентов
sudo easytier-core -i 10.144.144.1 --vpn-portal wg://0.0.0.0:11013/10.14.14.0/24
Получите конфигурацию для WireGuard-клиента:

bash
# Получение конфигурации WireGuard-клиента
easytier-cli vpn-portal
В полученной конфигурации:

Установите Interface.Address в свободный IP-адрес из подсети WireGuard

Установите Peer.Endpoint в публичный IP/доменное имя вашего узла EasyTier

Импортируйте изменённую конфигурацию в ваш WireGuard-клиент

Запуск собственного публичного общего узла
Вы можете запустить собственный публичный общий узел, чтобы помогать другим узлам обнаруживать друг друга. Публичный общий узел — это обычная сеть EasyTier (с теми же именем и ключом), к которой могут подключаться другие сети.

Для запуска публичного общего узла:

bash
# Публичному общему узлу не нужно указывать IPv4-адрес
sudo easytier-core --network-name mysharednode --network-secret mysharednode
После успешной настройки сети вы можете легко настроить её автоматический запуск при загрузке системы. Смотрите руководство по однокомандной регистрации в качестве службы для получения информации о регистрации EasyTier как системной службы.

Связанные проекты
ZeroTier: глобальная виртуальная сеть для подключения устройств.

TailScale: VPN-решение для упрощения настройки сети.

Связаться с нами
💬 Группа в Telegram

👥 Группы в QQ

Группа 1 949700262

Группа 2 837676408

Группа 3 957189589

Лицензия
EasyTier распространяется под лицензией LGPL-3.0.

Поддержка
Ускорение доставки контента (CDN) и защита этого проекта обеспечиваются спонсорством Tencent Cloud EdgeOne.

<p align="center"> <a href="https://edgeone.ai/?from=github" target="_blank"> <img src="assets/edgeone.png" width="200"> </a> </p>
Особая благодарность Langlangyun и Rainyun за спонсорство наших публичных серверов.

<p align="center"> <a href="https://langlangy.cn/?i26c5a5" target="_blank"> <img src="assets/langlang.png" width="200"> </a> <a href="https://langlangy.cn/?i26c5a5" target="_blank"> <img src="assets/raincloud.png" width="200"> </a> </p>
Если EasyTier оказался для вас полезен, рассмотрите возможность поддержки проекта. Разработка и поддержка программного обеспечения требуют много времени и усилий, и ваша поддержка поможет нам лучше развивать и улучшать EasyTier.

<p align="center"> <img src="assets/wechat.png" width="200"> <img src="assets/alipay.png" width="200"> </p> ```