```table-of-contents
title: Содержание:
style: nestedList # TOC style (nestedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 0 # Include headings up to the specified level
includeLinks: true # Make headings clickable
debugInConsole: false # Print debug info in Obsidian console
```
---
# Описание dnscrypt-proxy

`dnscrypt-proxy` — это гибкий DNS-прокси с поддержкой современных зашифрованных DNS-протоколов, таких, как DNSCrypt v2, DNS-over-HTTPS и Anonymized DNSCrypt.  
У программы открыт исходный код, также программа доступна в виде предварительно скомпилированных двоичных файлов для большинства операционных систем и архитектур.

Характеристики

- Шифрование и аутентификация DNS-трафика. Поддерживает DNS-over-HTTPS (DoH) с использованием TLS 1.3, DNSCrypt и анонимного DNS
- IP-адреса клиентов могут быть скрыты с помощью Tor, SOCKS-прокси или анонимных DNS-ретрансляторов
- Мониторинг DNS-запросов с отдельными файлами журналов для обычных и подозрительных запросов
- Фильтрация: блокируйте рекламу, вредоносное ПО и другой нежелательный контент. -
- Совместим со всеми службами DNS
- Фильтрация по времени с гибким недельным расписанием
- Прозрачное перенаправление определённых доменов на определённые резолверы
- Кэширование DNS для уменьшения задержки и повышения конфиденциальности
- Локальная блокировка IPv6 для уменьшения задержки в сетях только с IPv4
- Балансировка нагрузки: выберите набор резолверов, dnscrypt-proxy будет автоматически измерять и отслеживать их скорость, а также балансировать трафик между самыми быстрыми из доступных.
- Маскировка: как файл HOSTS на стероидах, который может возвращать предварительно настроенные адреса для определённых имён или разрешать и возвращать IP-адреса других имён. Это можно использовать для локальной разработки, а также для обеспечения безопасных результатов поиска в Google, Yahoo, DuckDuckGo и Bing.
- Автоматическое обновление списков резолверов в фоновом режиме
- Может заставить исходящие соединения использовать TCP
- Совместим с DNSSEC
- Включает локальный сервер DoH для поддержки ECHO (ESNI)

Домашняя страница: https://dnscrypt.info/

В первую очередь dnscrypt-proxy применяется в качестве постоянно работающей в фоне службы, к которой обращаются программы для преобразования имени хоста в IP адрес. Но также dnscrypt-proxy можно запустить как утилиту командной строки.
# Использование:

Опции:

`-check` - Проверить конфигурационный файл и выйти  
`-child` - Вызывает программу как дочерний процесс  
`-config СТРОКА [путь до файла]` - Путь до конфигурационного файла (по умолчанию "dnscrypt-proxy.toml")  
`-json` - Вывести список как JSON  
`-list` - Вывести список доступных преобразователей (резолверов) для включённых фильтров  
`-list-all` - Напечатать полный список доступных резолверов, игнорируя фильтры  
`-logfile СТРОКА [путь до файла]` - Записывать журнал приложения в указанный файл  
`-logfile-truncate` - Обрезать файл журнала приложения; хранить только данные о последнем запуске приложения  
`-loglevel ЗНАЧЕНИЕ` - Уровень журнала приложения (0-6) (по умолчанию 2)  
`-netprobe-timeout ЧИСЛО` - Переписать таймаут netprobe (по умолчанию 60)  
`-pidfile  СТРОКА [путь до файла]` - Если указан, записывать pid в этот файл  
`-resolve  СТРОКА` - Преобразовывать имя используя системные библиотеки  
`-service СТРОКА` - Управление системным сервисом: `start`, `stop`, `restart`, `install`, `uninstall`  
`-show-certs` - Распечатать хэши цепочки сертификатов DoH  
`-syslog` - Отправлять журналы приложений в локальный системный журнал (журнал событий (Eventlog) в Windows, системный журнал (syslog) в Unix)  
`-version` - Напечатать текущую версию прокси  
## Руководство по dnscrypt-proxy

Страница man отсутствует.
Конфигурационный файл dnscrypt-proxy

Ниже показан рабочий пример конфигурационного файла dnscrypt-proxy с пояснениями.
### Конфигурационный файл
```q
#-------------------------------------------#
#        конфигурация dnscrypt-proxy        #
#-------------------------------------------#

## Это пример конфигурационного файла.
## Вам следует подправить его под свои потребности и сохранить как "dnscrypt-proxy.toml"
##
## Онлайн документация доступна здесь: https://dnscrypt.info/doc

#------------------------------------#
#        Глобальные настройки        #
#------------------------------------#

## Список серверов для использования
##
## Сервера из источника "public-resolvers" (смотрите ниже) можно
## посмотреть здесь: https://dnscrypt.info/public-servers
##
## Прокси автоматически отберёт из этого списка рабочие сервера.
## Помните, что фильтры require_* НЕ применяются при использовании этих настроек.
##
## По умолчанию этот список пустой и вместо него будут использованы все
## зарегистрированные сервера, удовлетворяющие фильтрам require_*.
##
## В первую очередь удалите начальный # чтобы включить эту настройку; строки, начинающиеся с #, игнорируются.

# server_names = ['scaleway-fr', 'google', 'yandex', 'cloudflare']
# server_names = ['cloudflare']

## Список локальных адресов и портов для прослушивания. Могут быть IPv4 и/или IPv6.
## Пример при использовании IPv4 и IPv6:
## listen_addresses = ['127.0.0.1:53', '[::1]:53']
listen_addresses = ['127.0.0.1:53']

## Максимальное число одновременно принимаемых подключений от клиентов
max_clients = 250

## Переключиться на другого системного пользователя после того, как прослушивающий сокет был создан.
## Примечание (1): в настоящее время эта функция не поддерживается в Windows.
## Примечание (2): эта функция не совместима с активацией сокета systemd.
## Примечание (3): при использовании -pidfile, директория с файлом PID должна быть доступной для записи новому пользователю
# user_name = 'nobody'

## Определённые критерии, которым должны удовлетворять сервера (из статичных + удалённых источников)
## Использовать сервера, доступные по IPv4
ipv4_servers = true

## Использовать сервера, доступные по IPv6 — не включайте, если у вас нет IPv6 подключения
ipv6_servers = false

## Использовать сервера, реализующие DNSCrypt протокол
dnscrypt_servers = true

## Использовать сервера, реализующие DNS-over-HTTPS протокол
doh_servers = true

## Use servers implementing the Oblivious DoH protocol
odoh_servers = false

## Требовать, чтобы серверы, определённые удалёнными источниками, удовлетворяли определенным свойствам
## Сервер должен поддерживать расширения безопасности DNS (DNSSEC)
require_dnssec = false

## Сервера на должны вести журнал пользовательской активности (с их слов)
require_nolog = true

## Сервер не должен применять собственный чёрный список (для родительского контроля, блокировки рекламы и прочего)
require_nofilter = true

# Имена серверов, которые нужно избегать даже если они удовлетворяют всем критериям
disabled_server_names = []

## Всегда использовать TCP для подключения к вышестоящим серверам.
## Это может быть полезным, если вам нужно перенаправлять весь трафик через Tor.
## В противном случае, оставьте значение на `false`, поскольку это не улучшает безопасности
## (dnscrypt-proxy всегда шифрует всё, даже при использовании UDP), и можоет
## только увеличить время задержки.
force_tcp = false

## SOCKS прокси
## Раскомментируйте следующие строки для перенаправления всех TCP подключений к локальной ноде Tor
## Tor не поддерживает UDP, поэтому также установите `force_tcp` на `true`.
# proxy = 'socks5://127.0.0.1:9050'

## HTTP/HTTPS прокси
## Только для DoH серверов
# http_proxy = 'http://127.0.0.1:8888'

## Как долго DNS запрос будет ждать ответа, в миллисекундах.
## Если у вас сеть с *сильной* задержкой, вам может понадобиться
## увеличить это. Запуск может стать медленнее, если вы увеличите это.
## Не увеличивайте слишком сильно. 10000 это самая высокая разумная величина.
timeout = 5000

## Keepalive для HTTP (HTTPS, HTTP/2) запросов, в секундах
keepalive = 30

## Add EDNS-client-subnet information to outgoing queries
## Multiple networks can be listed; they will be randomly chosen.
## These networks don't have to match your actual networks.
# edns_client_subnet = ["0.0.0.0/0", "2001:db8::/32"]

## Ответ на заблокированные запросы.  Опции: `refused`, `hinfo` (по умолчанию) или
## определённый заранее IP.  Чтобы дать IP-ответ, используйте формат `a:<IPv4>,aaaa:<IPv6>`.
## Использование опции `hinfo` означает, что некоторые ответы будут ложью.
## К сожалению, опция `hinfo`, по видимому, требуется для Android 8+
# blocked_query_response = 'refused'

## Стратегия балансировки нагрузки: 'p2' (по умолчанию), 'ph', 'first' или 'random'
## Load-balancing strategy: 'p2' (default), 'ph', 'p<n>', 'first' or 'random'
## Randomly choose 1 of the fastest 2, half, n, 1 or all live servers by latency.
## The response quality still depends on the server itself.
# lb_strategy = 'p2'

## Установите значение `true`, чтобы постоянно пытаться оценить задержку всех резолверов.
## Default is `true` that makes 'p2' `lb_strategy` work well.
# lb_estimator = true

## Уровень ведения журнала (0-6, по умолчанию: 2. Вариант 0 это очень подробный, 6 содержит только фатальные ошибки)
# log_level = 2

## Файл журнала для приложения, альтернатива отправки записей журнала в
## стандартную службу системного журнала (syslog/Windows event log).
## Этот файл отличается от других файлов журнала, и не будет
## автоматически ротироваться приложением.
# log_file = '/var/log/dnscrypt-proxy/dnscrypt-proxy.log'

## При использовании файла журнала, хранить логи только с самого последнего запуска.
# log_file_latest = true

## Использовать системный логер (syslog на Unix, Event Log на Windows)
use_syslog = true

## Задержка, в минутах, после которой сертификаты перезагружаются
cert_refresh_delay = 240

## DNSCrypt: Создать новый, уникальный ключ для каждого отдельного DNS запроса
## Это может улучшить приватность, но также имеет значительное воздействие на использоцание центрального процессора
## Включайте только если у вас не слишком большая нагрузка на сеть
# dnscrypt_ephemeral_keys = false

## DoH: Отключить сессионные тикеты TLS — увеличивает приватность, но также и задержку
# tls_disable_session_tickets = false

## DoH: Использовать определённый набор шифров вместо предпочитаемого сервером
## 49199 = TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
## 49195 = TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
## 52392 = TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305
## 52393 = TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305
##  4865 = TLS_AES_128_GCM_SHA256
##  4867 = TLS_CHACHA20_POLY1305_SHA256
## На не-Intel ЦПУ, таких как роутеры MIPS и системы ARM (Android, Raspberry Pi...),
## следующий набор улучшает производительность.
## Он также может помочь на ЦПУ Intel CPU работающих с 32-битными операционными системами.
## Держите tls_cipher_suite пустым если у вас проблемы с получением источников или
## подключению к DoH серверам. Google и Cloudflare работают с ними нормально.
# tls_cipher_suite = [52392, 49199]

## Bootstrap resolvers
## These are normal, non-encrypted DNS resolvers, that will be only used
## for one-shot queries when retrieving the initial resolvers list and if
## the system DNS configuration doesn't work.
##
## No user queries will ever be leaked through these resolvers, and they will
## not be used after IP addresses of DoH resolvers have been found (if you are
## using DoH).
##
## They will never be used if lists have already been cached, and if the stamps
## of the configured servers already include IP addresses (which is the case for
## most of DoH servers, and for all DNSCrypt servers and relays).
##
## They will not be used if the configured system DNS works, or after the
## proxy already has at least one usable secure resolver.
##
## Resolvers supporting DNSSEC are recommended, and, if you are using
## DoH, bootstrap resolvers should ideally be operated by a different entity
## than the DoH servers you will be using, especially if you have IPv6 enabled.
##
## People in China may want to use 114.114.114.114:53 here.
## Other popular options include 8.8.8.8, 9.9.9.9 and 1.1.1.1.
##
## If more than one resolver is specified, they will be tried in sequence.
##
## TL;DR: put valid standard resolver addresses here. Your actual queries will
## not be sent there. If you're using DNSCrypt or Anonymized DNS and your
## lists are up to date, these resolvers will not even be used.
bootstrap_resolvers = ['9.9.9.9:53', '8.8.8.8:53']

## Всегда использовать запасные DNS сервера перед системными DNS настройками.
ignore_system_dns = true

## Максимальное время (в секундах) ожидания сетевого подключения перед
## инициализацией прокси.
## Полезно если прокси автоматически запускается при загрузке, а сетевое
## подключение не гарантировано немедленно доступно.
## Используйте 0 для выключения вовсе тестирования возможности подключения (не рекомендуется),
## и -1 для ожидания так долго, насколько это возможно.
netprobe_timeout = 60

## Адрес и порт, чтобы попытаться установить соединение, только для проверки
## работает ли сеть. Это может быть любой адрес и любой порт, даже если
## на другой стороне нечему ответить. Только не используйте
## локальный адрес, поскольку цель в проверке возможности подключения к Интернету.
## В Windows будет отправлена датаграмма с одним, nul байтом, только
## когда система запускается.
## На других операционных системах будет инициализировано подключение,
## но ничего не будет отправлено.
netprobe_address = '9.9.9.9:53'
#netprobe_address = '8.8.8.8:53'

## Офлайн режим — Не использовать никакие удалённые зашифрованные серверы.
## Сервер будет оставаться полностью функциональным для ответа на запросы, которые
## напрямую может обрабатывать плагин (forwarding, cloaking, ...)
# offline_mode = false

## Дополнительные данные для присоединения к исходящим запросам.
## Эта строка будет добавлена к запросам как TXT записи.
## Не используйте, кроме как на серверах, которые явно запрашивают присутствие
## дополнительных данных.
## encrypted-dns-server может быть настроен для использования этого в качестве контроля доступа
## в разделе [access_control]
# query_meta = ["key1:value1", "key2:value2", "token:MySecretToken"]

## Автоматическая ротация файлов журналов
## Максимальный размер файлов журналов в MB — Установите на 0 для неограниченного.
log_files_max_size = 10

## Как долго хранить хранить файлы резервных копий, в днях
log_files_max_age = 7

## Максимум хранимых копий резервных файлов (или 0 чтобы хранить все бэкапы)
log_files_max_backups = 1

#-----------------------#
#        Фильтры        #
#-----------------------#

## Примечание: если вы используете dnsmasq, то отключите опцию `dnssec` в dnsmasq если вы
## настроили dnscrypt-proxy делать любого рода фильтрацию (включая фильтры
## ниже и чёрные списки).
## Вы ещё можете выбрать резолверы, которые делают DNSSEC валидацию.

## Немедленно ответить на связанные с IPv6 запросы пустым ответом
## Это ускоряет когда нет IPv6 подключения, но также может
## проблемы с надёжностью на некоторых серверах-заглушках.
block_ipv6 = false

## Немедленно отвечать на запросы A и AAAA для имён хостов без имени домена
block_unqualified = true

## Немедленно отвечать на запросы для local zones вместо того, чтобы выпускать их на вышестоящие
## преобразователи имён (такие запросы в любом случае всегда вызывают ошибки или тайм-ауты).
block_undelegated = true

## TTL для синтетических ответов, отправленных, когда запрос был заблокирован (из-за
## IPv6 или чёрных списков).
reject_ttl = 10

#----------------------------------------------------------------------------------------#
#        Направлять запросы для определенных доменов на выделенный набор серверов        #
#----------------------------------------------------------------------------------------#

## Смотрите примеры в файле `example-forwarding-rules.txt`
# forwarding_rules = '/etc/dnscrypt-proxy/forwarding-rules.txt'

#--------------------------------#
#        Cloaking правила        #
#--------------------------------#

## Маскировка (cloaking) возвращает предопределённый адрес для определённого имени.
## В дополнении к действию как HOSTS файл, программа также может вернуть IP адрес
## другого имени. Программа также выполнит выравнивание CNAME.

## Смотрите примеры в файле `example-cloaking-rules.txt`
# cloaking_rules = '/etc/dnscrypt-proxy/cloaking-rules.txt'

## TTL используемый когда ответы отправлены с задействованием файла cloaking-rules.txt
# cloak_ttl = 600

#-----------------------#
#        DNS кэш        #
#-----------------------#

## Включить DNS для уменьшения задержки и исходящего трафика
cache = true

## Размер кэша
cache_size = 4096

## Минимальное TTL для кэшированных записей
cache_min_ttl = 2400

## Максимальное TTL для кэшированных записей
cache_max_ttl = 86400

## Минимальное TTL для негативно кэшированных записей
cache_neg_min_ttl = 1

## Максимальное TTL для негативно кэшированных записей
cache_neg_max_ttl = 60

#---------------------------------------#
#        Captive portal handling        #
#---------------------------------------#

[captive_portals]

## A file that contains a set of names used by operating systems to
## check for connectivity and captive portals, along with hard-coded
## IP addresses to return.
# map_file = '/etc/dnscrypt-proxy/example-captive-portals.txt'

#------------------------------------#
#        Локальный DoH сервер        #
#------------------------------------#

[local_doh]

## dnscrypt-proxy может работать как локальный DoH сервер. Таким образом, веб-браузеры,
## требующие прямого подключения к серверу DoH для включения некоторых
## функций, будут включать их, не обходя ваш прокси-сервер DNS.

## Адрес, который должен прослушивать локальный DoH сервер
# listen_addresses = ['127.0.0.1:3000']


## Путь до URL DoH. Это не файл, а путь после имени хоста
## в URL. По соглашению, часто выбирается `/dns-query`.
## Для каждого `listen_address` полный URL для доступа к серверу будет:
## `https://<АДРЕС_ПРОСЛУШИВАНИЯ><ПУТЬ>` (например: `https://127.0.0.1/dns-query`)
# path = "/dns-query"


## Файл сертификата и ключ — Помните, что сертификат должен быть в доверенных.
## Смотрите документацию (wiki) для дополнительной информации.
# cert_file = "/var/lib/dnscrypt-proxy/localhost.pem"
# cert_key_file = "/var/lib/dnscrypt-proxy/localhost.pem"

#----------------------------------------#
#        Ведение журнала запросов        #
#----------------------------------------#

## Записывать клиентские запросы в файл
[query_log]

  ## Путь до файла журнала запросов (абсолютный или относительный к той же самой директории, где конфигурационный файл)
  ## На не-Windows системах, может быть /dev/stdout для вывода журнала в стандартный вывод (также установите log_files_max_size на 0)
  # file = '/var/log/dnscrypt-proxy/query.log'

  ## Формат журнала запросов (в настоящее время поддерживаются: tsv и ltsv)
  format = 'tsv'

  ## Не записывать в журнал эти типы запросов для уменьшения подробности. Оставьте пустым для записи всего.
  # ignored_qtypes = ['DNSKEY', 'NS']

#-------------------------------------------------------#
#        Запись в журнал подозрительных запросов        #
#-------------------------------------------------------#

## Журнал запросов несуществующих зон
## Эти запросы могут раскрыть присутствие вредоносного ПО, сломанных/устаревших приложений,
## и устройств, сигнализирующих о своём присутствии третьим сторонам.

[nx_log]

  ## Путь до файла журнала запросов (абсолютный или относительный к той же самой директории, где конфигурационный файл)
  # file = '/var/log/dnscrypt-proxy/nx.log'

  ## Формат журнала запросов (в настоящее время поддерживаются: tsv и ltsv)
  format = 'tsv'

#-------------------------------------------------------------#
#        Блокировка на основе шаблонов (чёрные списки)        #
#-------------------------------------------------------------#

## Чёрные списки сделаны как один шаблон на строку. Примеры действительных шаблонов:
##
##   example.com
##   =example.com
##   *sex*
##   ads.*
##   ads*.example.*
##   ads*.example[0-9]*.com
##
## Примеры файлов чёрных списков могут быть найдены в https://download.dnscrypt.info/blacklists/
## Скрипт для сборки чёрных список из публичных фидов может быть найден в директории
## `utils/generate-domains-blacklists` исходного кода dnscrypt-proxy.

[blocked_names]

  ## Путь до файла с правилами блокировки (абсолютный или относительный к той же самой директории, где конфигурационный файл)
  # blocked_names_file = '/etc/dnscrypt-proxy/blocked-names.txt'

  ## Опциональный путь к файлу ведения журнала заблокированных запросов
  # log_file = '/var/log/dnscrypt-proxy/blocked-names.log'

  ## Необязательный формат журнала: tsv или ltsv (по умолчанию: tsv)
  # log_format = 'tsv'

#----------------------------------------------------------------------#
#        Блокировка по IP на основе шаблонов (чёрный список IP)        #
#----------------------------------------------------------------------#

## Чёрные списки IP делаются в виде одного шаблона на строку. Примеры действительных шаблонов:
##
##   127.*
##   fe80:abcd:*
##   192.168.1.4

[blocked_ips]

  ## Путь до файла с правилами блокировки (абсолютный или относительный к той же самой директории, где конфигурационный файл)
  # blocked_ips_file = '/etc/dnscrypt-proxy/blocked-ips.txt'

  ## Опциональный путь к файлу ведения журнала заблокированных запросов
  # log_file = '/var/log/dnscrypt-proxy/blocked-ips.log'

  ## Необязательный формат журнала: tsv или ltsv (по умолчанию: tsv)
  # log_format = 'tsv'

#---------------------------------------------------------------------------#
#        Белые списки на основе шаблонов (списки разрешённых сайтов)        #
#---------------------------------------------------------------------------#

## Белые списки поддерживают те же шаблоны, что и чёрные списки
## Если имя совпадает с записью в белом списке, соответствующая сессия
## обойдёт фильтры имён и IP.
##
## Также поддерживаются правила, основанные на времени, чтобы некоторые веб-сайты были доступны только в определённое время дня.

[allowed_names]

  ## Путь до файла с правилами белого списка (абсолютный или относительный к той же самой директории, где конфигурационный файл)
  # allowed_names_file = '/etc/dnscrypt-proxy/allowed-names.txt'

  ## Опциональный путь к файлу ведения журнала заблокированных запросов
  # log_file = '/var/log/dnscrypt-proxy/allowed-names.log'

  ## Необязательный формат журнала: tsv или ltsv (по умолчанию: tsv)
  # log_format = 'tsv'

#-------------------------------------------------------------------#
#        Pattern-based allowed IPs lists (blocklists bypass)        #
#-------------------------------------------------------------------#

## Allowed IP lists support the same patterns as IP blocklists
## If an IP response matches an allow ip entry, the corresponding session
## will bypass IP filters.
##
## Time-based rules are also supported to make some websites only accessible at specific times of the day.

[allowed_ips]

  ## Path to the file of allowed ip rules (absolute, or relative to the same directory as the config file)
  # allowed_ips_file = '/etc/dnscrypt-proxy/allowed-ips.txt'

  ## Optional path to a file logging allowed queries
  # log_file = '/var/log/dnscrypt-proxy/allowed-ips.log'

  ## Optional log format: tsv or ltsv (default: tsv)
  # log_format = 'tsv'

#----------------------------------------------#
#        Ограничения доступа по времени        #
#----------------------------------------------#

## Здесь можно определить одно или несколько недельных расписаний.
## Шаблоны в списке блокировки основанном на именах могут опционально быть дополнены строкой @ИМЯ_РАСПИСАНИЯ
## для применения шаблона 'ИМЯ_РАСПИСАНИЯ' только когда он совпадает с интервалом времени этого расписания.
##
## Например, следующее правило в файле чёрного списка:
## *.youtube.* @time-to-sleep
## заблокирует доступ на YouTube в период времени, определённый расписанием 'time-to-sleep'.
##
## {after='21:00', before= '7:00'} сработает в 0:00-7:00 и 21:00-0:00
## {after= '9:00', before='18:00'} сработает в 9:00-18:00

[schedules]

  # [schedules.'time-to-sleep']
  # mon = [{after='21:00', before='7:00'}]
  # tue = [{after='21:00', before='7:00'}]
  # wed = [{after='21:00', before='7:00'}]
  # thu = [{after='21:00', before='7:00'}]
  # fri = [{after='23:00', before='7:00'}]
  # sat = [{after='23:00', before='7:00'}]
  # sun = [{after='21:00', before='7:00'}]

  # [schedules.'work']
  # mon = [{after='9:00', before='18:00'}]
  # tue = [{after='9:00', before='18:00'}]
  # wed = [{after='9:00', before='18:00'}]
  # thu = [{after='9:00', before='18:00'}]
  # fri = [{after='9:00', before='17:00'}]

#-----------------------#
#        Серверы        #
#-----------------------#

## Удалённые списки доступных серверов
## Одновременно можно использовать несколько источников, но каждый источник
## требует выделенного файла кэша.
##
## Обратитесь к документации по URL публичных источников.
##
## К именам серверов может быть добавлен префикс, чтобы
## исключить коллизии, если одинаковые сервера встречают н
## различных источниках. В этом случае имена, перечисленные в `server_names`
## должны включать эти префисы.
##
## Если свойство `urls` отсутствует, файлы кэша и действительных подписей
## уже должны присутствовать. Это не предотвращает эти файлы кэша от
## истечения срока годности после `refresh_delay` часов.

[sources]

  ## Пример удалённого источника от https://github.com/DNSCrypt/dnscrypt-resolvers

  [sources.'public-resolvers']
    urls = ['https://raw.githubusercontent.com/DNSCrypt/dnscrypt-resolvers/master/v3/public-resolvers.md', 'https://download.dnscrypt.info/resolvers-list/v3/public-resolvers.md', 'https://ipv6.download.dnscrypt.info/resolvers-list/v3/public-resolvers.md', 'https://download.dnscrypt.net/resolvers-list/v3/public-resolvers.md']
    cache_file = '/var/cache/dnscrypt-proxy/public-resolvers.md'
    minisign_key = 'RWQf6LRCGA9i53mlYecO4IzT51TGPpvWucNSCh1CBM0QTaLn73Y7GFO3'
    refresh_delay = 72
    prefix = ''

  ## Анонимизированные DNS-ретранслятор

  [sources.'relays']
    urls = ['https://raw.githubusercontent.com/DNSCrypt/dnscrypt-resolvers/master/v3/relays.md', 'https://download.dnscrypt.info/resolvers-list/v3/relays.md', 'https://ipv6.download.dnscrypt.info/resolvers-list/v3/relays.md', 'https://download.dnscrypt.net/resolvers-list/v3/relays.md']
    cache_file = '/var/cache/dnscrypt-proxy/relays.md'
    minisign_key = 'RWQf6LRCGA9i53mlYecO4IzT51TGPpvWucNSCh1CBM0QTaLn73Y7GFO3'
    refresh_delay = 72
    prefix = ''


  ## Quad9 через DNSCrypt - https://quad9.net/

  # [sources.quad9-resolvers]
  #   urls = ['https://www.quad9.net/quad9-resolvers.md']
  #   minisign_key = 'RWQBphd2+f6eiAqBsvDZEBXBGHQBJfeG6G+wJPPKxCZMoEQYpmoysKUN'
  #   cache_file = '/var/cache/dnscrypt-proxy/quad9-resolvers.md'
  #   prefix = 'quad9-'

  ## Другой пример источника, с резолверами, цензурирующими некоторые веб-сайты, не подходящие для детей.
  ## Это подмножество списка `public-resolvers`, поэтому включение обоих бесполезно

  #  [sources.'parental-control']
  #    urls = ['https://raw.githubusercontent.com/DNSCrypt/dnscrypt-resolvers/master/v3/parental-control.md', 'https://download.dnscrypt.info/resolvers-list/v3/parental-control.md', 'https://ipv6.download.dnscrypt.info/resolvers-list/v3/parental-control.md', 'https://download.dnscrypt.net/resolvers-list/v3/parental-control.md']
  #    cache_file = '/var/cache/dnscrypt-proxy/parental-control.md'
  #    minisign_key = 'RWQf6LRCGA9i53mlYecO4IzT51TGPpvWucNSCh1CBM0QTaLn73Y7GFO3'

#-------------------------------------------#
#        Серверы с известными багами        #
#-------------------------------------------#

[broken_implementations]

# В настоящее время серверы Cisco не могут обрабатывать запросы размером более 1472 байтов и не
#  усекают ответы, размер которых превышает размер запросов, как того требует протокол DNSCrypt.
# Это предотвращает получение больших ответов по UDP и через ретранслятор.
#
# По сервера `dnsdist` отбрасывает запросы клиентов больше чем 1500 байт.
# Они это знают и работают над исправлением.
#
# Приведённый ниже костыль позволяет сделать использование без ретрансляторов более надёжным
# пока указанные серверы не исправлены.

fragments_blocked = ['cisco', 'cisco-ipv6', 'cisco-familyshield', 'cisco-familyshield-ipv6', 'cleanbrowsing-adult', 'cleanbrowsing-adult-ipv6', 'cleanbrowsing-family', 'cleanbrowsing-family-ipv6', 'cleanbrowsing-security', 'cleanbrowsing-security-ipv6']

#---------------------------------------------------------------------#
#        Аутентификация клиентов на основе сертификата для DoH        #
#---------------------------------------------------------------------#

# Используйте X509 сертификат для аутентификации себя когда подключаетесь к серверам DoH.
# Это полезно только если вы работаете со своим собственным, приватным DoH сервером.
# 'creds' сопоставляет сервера к сертификатам, и поддерживает множество записей.
# Если вы не используете стандартные корневые CA, опциональное свойство "root_ca"
# устанавливает путь до файла CRT, его можно добавить к записи о сервере.

[doh_client_x509_auth]

#
# creds = [
#    { server_name='myserver', client_cert='client.crt', client_key='client.key' }
# ]

#-----------------------------#
#        Анонимный DNS        #
#-----------------------------#

[anonymized_dns]

## Маршруты — это косвенные способы доступа к серверам DNSCrypt.
##
## Маршрут сопоставляет имя сервера («имя_сервера») одному или нескольким ретранслятор, которые
## будут использоваться для подключения к этому серверу.
##
## Ретранслятор может быть указан как DNS Stamp (как relay stamp или
## DNSCrypt stamp), IP:port, ИМЯ_ХОСТА:ПОРТ или имя сервера.
##
## Следующие примеры маршрутов "example-server-1" через `anon-example-1` или `anon-example-2`,
## and "example-server-2" через через ретранслятор чей ретранслятор имеет DNS stamp
## "sdns://gRIxMzcuNzQuMjIzLjIzNDo0NDM".
##
## !!! ЭТО ПРОСТО ПРИМЕРЫ !!!
##
## Просмотрите список доступных ретрансляторов в файле «relays.md» и для каждого сервера, который

## вы хотите использовать, определите ретранслятор, через которые будут проходить соединения.
##
## Тщательно выбирайте ретрансляторы и серверы, чтобы они управлялись разными юридическими лицами.
##
## "server_name" также может быть установлено "*" для определения маршрута по умолчанию, но это не
## рекомендуется. Если вы так делаете, храните "server_names" коротким и отличным от ретрансляторов.

# routes = [
#    { server_name='example-server-1', via=['anon-example-1', 'anon-example-2'] },
#    { server_name='example-server-2', via=['sdns://gRIxMzcuNzQuMjIzLjIzNDo0NDM'] }
# ]

## пропустить резолверы, несовместимые с анонимизацией, вместо того, чтобы использовать их напрямую
skip_incompatible = false

# If public server certificates for a non-conformant server cannot be
# retrieved via a relay, try getting them directly. Actual queries
# will then always go through relays.

# direct_cert_fallback = false

#---------------------#
#        DNS64        #
#---------------------#

## DNS64 — это механизм для синтеза записей AAAA из записей A.
## Он используется с транслятором IPv6/IPv4 для включения клиент-сервер
## коммуникации между только IPv6 клиентом и только IPv4 сервером,
## не требуя никаких изменений как на IPv6, так и на IPv4 узле,
## для класса приложений, которые работают через NAT.
##
## Имеется две опции для синтеза таких записей:
## Опция 1: Используя набор статичных IPv6 префиксов;
## Опция 2: Путём обнаружения IPv6 префиксов из резолверов с поддержкой DNS64.
##
## Если настроены обе опции, то используются только статичные префиксы.
## (Ref. RFC6147, RFC6052, RFC7050)
##
## Не включайте, если вы не знаете что такое DNS64 и почему вам это нужно, иначе
## вы вообще не сможете ни к чему подключиться.

[dns64]

## (Опция 1) Статичный префикс(ы) как Pref64::/n в CIDR.
# prefix = ["64:ff9b::/96"]

## (Опция 2) Резолвер(ы) с включённым DNS64 для обнаружения Pref64::/n CIDR.
## Эти резолверы используются для запросов только Well-Known IPv4 Name (WKN) "ipv4only.arpa." только для обнаружения.
## Установите с резолверами вашего ISP в случае ваших собственных префиксов (отличный от Well-Known Prefix 64:ff9b::/96).
## ВАЖНО: Дефолтные резолверы перечисленные ниже поддерживают только Well-Known Prefix 64:ff9b::/96.
# resolver = ["[2606:4700:4700::64]:53", "[2001:4860:4860::64]:53"]

#--------------------------------#
#        Статичные записи        #
#--------------------------------#

## Опциональный, локальный, статичный список дополнительных серверов
## Больше всего полезен для тестирования ваших собственных серверов

[static]

  # [static.'myserver']
  # stamp = 'sdns://AQcAAAAAAAAAAAAQMi5kbnNjcnlwdC1jZXJ0Lg'
```

Примеры запуска dnscrypt-proxy

>Вывести список используемых преобразователей (DNS серверов) (-list) на основе указанного конфигурационного файла (/etc/dnscrypt-proxy/dnscrypt-proxy.toml) — список формируется с учётом фильтров, установленных в конфигурационном файле, то есть это перечень фактически используемых DNS серверов для преобразования запросов в системе:
```shell
sudo dnscrypt-proxy -list -config /etc/dnscrypt-proxy/dnscrypt-proxy.toml
```

Пример вывода:  
`google`

>Установка в deb-дистрибутив
```shell
sudo apt install dnscrypt-proxy
```

>Установка в Arch, Manjaro
```shell
sudo pacman -S dnscrypt-proxy
```

> Разрешить автозагрузку службы
```shell
sudo systemctl enable dnscrypt-proxy.service
```

>Запустить службу
```shell
sudo systemctl start dnscrypt-proxy.service
```

>Остановить службу
```shell
sudo systemctl stop dnscrypt-proxy.service
```

>Запретить автозагрузку службы
```shell
sudo systemctl disable dnscrypt-proxy.service
```

>Редактирование конфигурации
```shell
sudo nano /etc/dnscrypt-proxy/dnscrypt-proxy.toml
```

>Файл */etc/resolv.conf*
должен содержать только 
 nameserver 127.0.0.1
```shell
sudo echo nameserver 127.0.0.1 > /etc/resolv.conf
```
  
>Запретить изменение (иммунитет) (chattr -i сбросить)     
```shell
sudo chattr +i /etc/resolv.conf
```
### Возможные проблемы
При обновлении пакета листнер сокета  может поменяться на `ListenStream=127.0.2.1:53` вместо `ListenStream=127.0.0.1:53`, такое наблюдается на Kali Linux.

>Достаточно имея root права поменять его в сервисе сокета по адресу `/lib/systemd/system/dnscrypt-proxy.socket `и перезапустить службу
```shell
sudo systemctl restart dnscrypt-proxy.socket
```

>Проверка работы
```shell
sudo dnscrypt-proxy -resolve ya.ru -config /etc/dnscrypt-proxy/dnscrypt-proxy.toml
```

>Проверка кто слушает 53 порт
```shell
sudo lsof -i :53
```

>Запретить от прослушивание 53 порта
```shell
sudo systemctl stop systemd-resolved.service
```

ВАЖНО! В загрузке должен быть только сервис `dnscrypt-proxy.service`, а не сокет `dnscrypt-proxy.socket`.
## Проверка утечки DNS
   https://www.dnsleaktest.com/