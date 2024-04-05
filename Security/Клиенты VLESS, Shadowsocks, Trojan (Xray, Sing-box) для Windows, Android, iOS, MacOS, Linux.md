
12 January 2024 · 6 min

Table of Contents

- [Логика работы](https://itdog.info/klienty-vless-shadowsocks-trojan-xray-sing-box-dlya-windows-android-ios-macos-linux/#%d0%bb%d0%be%d0%b3%d0%b8%d0%ba%d0%b0-%d1%80%d0%b0%d0%b1%d0%be%d1%82%d1%8b)
- [Android](https://itdog.info/klienty-vless-shadowsocks-trojan-xray-sing-box-dlya-windows-android-ios-macos-linux/#android)
    - [v2rayNG](https://itdog.info/klienty-vless-shadowsocks-trojan-xray-sing-box-dlya-windows-android-ios-macos-linux/#v2rayng)
    - [NekoBox](https://itdog.info/klienty-vless-shadowsocks-trojan-xray-sing-box-dlya-windows-android-ios-macos-linux/#nekobox)
- [iOS](https://itdog.info/klienty-vless-shadowsocks-trojan-xray-sing-box-dlya-windows-android-ios-macos-linux/#ios)
    - [Streisand](https://itdog.info/klienty-vless-shadowsocks-trojan-xray-sing-box-dlya-windows-android-ios-macos-linux/#streisand)
    - [FoXray](https://itdog.info/klienty-vless-shadowsocks-trojan-xray-sing-box-dlya-windows-android-ios-macos-linux/#foxray)
    - [Shadowrocket](https://itdog.info/klienty-vless-shadowsocks-trojan-xray-sing-box-dlya-windows-android-ios-macos-linux/#shadowrocket)
    - [V2Box - V2ray Client](https://itdog.info/klienty-vless-shadowsocks-trojan-xray-sing-box-dlya-windows-android-ios-macos-linux/#v2box---v2ray-client)
- [Windows](https://itdog.info/klienty-vless-shadowsocks-trojan-xray-sing-box-dlya-windows-android-ios-macos-linux/#windows)
    - [Furious](https://itdog.info/klienty-vless-shadowsocks-trojan-xray-sing-box-dlya-windows-android-ios-macos-linux/#furious)
    - [InvisibleMan-XRayClient](https://itdog.info/klienty-vless-shadowsocks-trojan-xray-sing-box-dlya-windows-android-ios-macos-linux/#invisibleman-xrayclient)
    - [Nekoray](https://itdog.info/klienty-vless-shadowsocks-trojan-xray-sing-box-dlya-windows-android-ios-macos-linux/#nekoray)
- [MacOS](https://itdog.info/klienty-vless-shadowsocks-trojan-xray-sing-box-dlya-windows-android-ios-macos-linux/#macos)
    - [V2Box - V2ray Client](https://itdog.info/klienty-vless-shadowsocks-trojan-xray-sing-box-dlya-windows-android-ios-macos-linux/#v2box---v2ray-client-1)
    - [FoXray](https://itdog.info/klienty-vless-shadowsocks-trojan-xray-sing-box-dlya-windows-android-ios-macos-linux/#foxray-1)
    - [Streisand](https://itdog.info/klienty-vless-shadowsocks-trojan-xray-sing-box-dlya-windows-android-ios-macos-linux/#streisand-1)
    - [V2RayXS](https://itdog.info/klienty-vless-shadowsocks-trojan-xray-sing-box-dlya-windows-android-ios-macos-linux/#v2rayxs)
    - [NekoRay/NekoBox for macOS](https://itdog.info/klienty-vless-shadowsocks-trojan-xray-sing-box-dlya-windows-android-ios-macos-linux/#nekoraynekobox-for-macos)
    - [Furious](https://itdog.info/klienty-vless-shadowsocks-trojan-xray-sing-box-dlya-windows-android-ios-macos-linux/#furious-1)
- [Linux](https://itdog.info/klienty-vless-shadowsocks-trojan-xray-sing-box-dlya-windows-android-ios-macos-linux/#linux)

Клиенты, которые можно настроить через clipboard строку и QR-код. На выходе получаем стандартный VPN, который пускает весь трафик через туннель. Либо получаем proxy, который можно использовать в приложениях.

# Логика работы

У вас должна быть так называемая clipboard string, выглядит примерно так:

```
ss://MjAyMi1ibGFrZTMtYWVzLTEyOC1nY206b25hRzU5RlVYTXFNUG94MmhPaWltZz09Cg==@itdog.info:443#good-proxy
```

Либо QR-код, который содержит эту же строку.

В этой строке заданные данные для подключения к proxy-серверу.

Вам нужно лишь сделать её импорт в приложение. Во всех приложениях это называется примерно “Add config from clipboard”. Приложение само берёт из буфера обмена строку, либо вам нужно её вставить в поле.

После импорта у вас появится подключение. Обычно его нужно выделить и нажать кнопку снизу. Либо в десктопных приложениях правой кнопкой на подключение и в контекстном меню выбрать “Start”. Подключений может быть несколько. И между ними можно легко переключаться.

# Android

## v2rayNG

[Google Play](https://play.google.com/store/apps/details?id=com.v2ray.ang)

[GitHub](https://github.com/2dust/v2rayNG)

Поддерживает: Vmess, VLESS, Shadowsocks, Shadowsocks2022, Socks, Trojan.

Плюсы:

- Есть в Google Play
- Бесплатный

Минусы:

- Плохо работает, если есть потери до сервера (10%)
- Не работает на некоторых телефонах Samsung. В этом [issue](https://github.com/2dust/v2rayNG/issues/2368) говорят, что проблема с версией в Google Play и надо скачать прямо из GitHub.
- Не заработал на двух современных ТВ-приставках на Android. (За этот фидбэк и про Samsung спасибо моему подписчику)
- У меня не работает UDP. Это делает его неработоспособным, если выключено шифрование DNS на телефоне

## NekoBox

[Google Play](https://play.google.com/store/apps/details?id=moe.nb4a)

[GitHub](https://github.com/MatsuriDayo/NekoBoxForAndroid)

[Подробный мануал по установке и настройке NekoBox](https://itdog.info/ustanovka-nekobox-na-android-iz-apk-fajla-nastrojka-podklyuchenij/)

Поддерживает: Vmess, VLESS, Shadowsocks, Shadowsocks2022, Socks, Trojan, Trojan Go, Http, NaïveProxy, Hysteria, TUIC, WireGuard, ShadowTLS, SSH. Также можно настроить цепочку прокси прям в приложении.

Плюсы:

- Работает при потерях до сервера (10%)
- Видно, что приложение вылизано, удобное прям
- Очень много всего умеет
- Есть в Google Play

Минусы:

- Сложно назвать это минусом, всем нужно что-то кушать. В Google Play оно стоит 7.5 евро

Но можно скачать бесплатно без смс прям из гитхаба. Автообновлений в этом случае не будет, но зайти раз в пару месяцев вручную обновится несложно.

Рекомендую использовать именно этот клиент.

Если у вас доступна покупка приложений и есть эти 7.5 евро, то рекомендую купить. Приложение стоит того, и вы поддержите автора.

Я по фану попробовал SSH подключение (в приложении это реализовано как VPN, но через SSH), завёлся и работает. Конечно, по скорости до SS2022 далеко, но суть в другом, это может быть простым запасным вариантом на будущее.

# iOS

## Streisand

Доступно для iOS, iPadOS, MacOS

[https://apps.apple.com/ru/app/streisand/id6450534064](https://apps.apple.com/ru/app/streisand/id6450534064)

Бесплатно.

- Обязательно нужно указать fingerprint для VLESS

На мой взгляд лучший бесплатный клиент.

## FoXray

Доступно для iOS, MacOS, iPadOS

[https://apps.apple.com/ru/app/foxray/id6448898396](https://apps.apple.com/ru/app/foxray/id6448898396)

Бесплатно. Есть premium версия. Стоит 200р, открывает какие-то дополнительные возможности. Для базового использования хватает бесплатной версии.

- Для SS нужна опция ‘UDP over TCP’
- Для удаления, шеринга и копирования конфига нужно свайпать влево. Не очевидно, хоть и написано сверху
- Работает с сервером VLESS на Sing-box только по TCP. Не идут DNS запросы. При переключении DNS в настройках на `https://1.1.1.1/dns-querу` начинает работать. В описании у них только про работу с XRay идёт речь и с ним работает без проблем. Видимо, есть какая-то проблема совместимости XRay и Sing-box, но в других клиентах XRay DNS по UDP как-то работает. Разработчик предложил решать это на стороне Sing-box.

UI не по мне и надписи “premium” мозолят глаза. А так хороший клиент.

## Shadowrocket

Доступно для iOS, iPadOS

[https://apps.apple.com/ru/app/shadowrocket/id932747118](https://apps.apple.com/ru/app/shadowrocket/id932747118)

Стоит 250р

- Для SS нужна опция ‘UDP over TCP’
- Добавление конфига через clipboard string организовано нативно. Если в буфере есть строка - предлагает вставить

Хороший клиент, своих 250р стоит.

## V2Box - V2ray Client

Доступно для iOS, MacOS, iPadOS

[https://apps.apple.com/ru/app/v2box-v2ray-client/id6446814690](https://apps.apple.com/ru/app/v2box-v2ray-client/id6446814690)

- Обязательно нужно указать fingerprint для VLESS

Мне нравился этот клиент. Раньше я его советовал и для MacOS и для iOS. Но теперь стала показываться реклама. Довольно часто и её нельзя отключить. Почему нет опции “заплати и пользуйся без рекламы” непонятно. В её текущем виде для iOS не рекомендую.

Надеюсь, разработчик исправит это, жалко такой красивый клиент.

# Windows

Под десктоп с клиентами для VLESS/SS2022 не очень хорошо. Особенно это ощущается после клиентов WireGuard и OpenVPN.

Есть вещь, которую надо понимать, при работе со всеми этими клиентами. Существует два режима работы:

- **Режим туннеля**, он же tun режим, он же VPN-режим. При его использовании вообще весь трафик с компьютера, в том числе, например, ping из cmd отправляется через туннель. Здесь происходит “встраивание” в систему на уровне таблицы маршрутизации. Поэтому для этого режима необходимы “права администратора”. Приложение всегда должно запускаться из-под админа.
    
- **Режим прокси**. Который, в свою очередь, делится на два вида:
    

1. Системный прокси, при нём все приложения, в которых по умолчанию стоит “использовать системный прокси” будут ходить через прокси.
2. Сам по себе. Просто поднимается прокси на определённом порту, и вы можете в нужных приложениях прописать, чтоб они проксировались, например, через localhost:123, и только эти приложения будут ходить через прокси.

Выделяется Nekoray, но ему далеко до понятного и удобного UI. Поэтому перечислю все клиенты, заработавшие у меня. Кстати, объединяет их всех отсутствие инсталлера, будьте готовы создавать ярлычки руками.

## Furious

[https://github.com/LorenEteval/Furious](https://github.com/LorenEteval/Furious)

- Внутри Xray-core
- Работает только в режиме системного прокси
- Активирование прокси только через трей. Кнопка **Connect**
- Настраивается там же, для РФ лучше выбрать **Global**
- Можно редактировать конфиг
- Не поддерживает SS2022. Поддерживает VLESS+reality

## InvisibleMan-XRayClient

[https://github.com/InvisibleManVPN/InvisibleMan-XRayClient](https://github.com/InvisibleManVPN/InvisibleMan-XRayClient)

- Внутри Xray-core
- Работает только в proxy режиме. Есть tun, но у меня он не заработал
- Редактирование конфига через текстовый редактор
- Не поддерживает SS2022. Поддерживает VLESS+reality

## Nekoray

[https://github.com/MatsuriDayo/nekoray/](https://github.com/MatsuriDayo/nekoray/)

- Внутри на выбор есть Xray-core и Sing-box, советую выбирать Sing-box
- Работает в обоих режимах
- Но не запоминает, какой последний был режим, поэтому придётся каждый раз тыкать галочку
- Активируется из контекстного меню, либо из трея
- Можно редактировать конфиги
- Поддерживает и SS2022 и VLESS+reality

# MacOS

У меня нет MacOS. Поэтому отзывы на MacOS привествуются особенно.

## V2Box - V2ray Client

[https://apps.apple.com/ru/app/v2box-v2ray-client/id6446814690](https://apps.apple.com/ru/app/v2box-v2ray-client/id6446814690)

Рабочее решение. Рекламы, кстати, в версии для MacOS у него нет.

## FoXray

[https://apps.apple.com/ru/app/foxray/id6448898396](https://apps.apple.com/ru/app/foxray/id6448898396)

Рабочее решение. UI, как и для iOS, специфичный.

## Streisand

[https://apps.apple.com/ru/app/streisand/id6450534064](https://apps.apple.com/ru/app/streisand/id6450534064)

Рабочее решение

## V2RayXS

[https://github.com/tzmax/V2RayXS](https://github.com/tzmax/V2RayXS)

## NekoRay/NekoBox for macOS

[https://github.com/abbasnaqdi/nekoray-macos](https://github.com/abbasnaqdi/nekoray-macos)

Рабочее решение

## Furious

[https://github.com/LorenEteval/Furious/](https://github.com/LorenEteval/Furious/)

Для винды рабочее решение, вероятно тут тоже всё окей. Но без tun режима.

# Linux

Единственный клиент с UI, который у меня заработал под Linux - это Nekoray. [https://github.com/MatsuriDayo/nekoray/](https://github.com/MatsuriDayo/nekoray/)

Всё так же работает как и под Windows. Но есть одно различие, это запуск от рута для tun режима. В Windows это указывается в свойствах ярлыка или самого exe-шника.

А, например, в Gnome, если приложению нужно что-то запустить\изменить от sudo, выводится окошко с запросом пароля. Тут при активации tun-режима это окно выводится **три раза** подряд. Это подбешивает 🙂

Изучаем issues на гитхабе проекта: [https://github.com/MatsuriDayo/nekoray/issues/759](https://github.com/MatsuriDayo/nekoray/issues/759)

У человека Ubuntu. Закрыто со статусом “not planned” без объяснений.

[https://github.com/MatsuriDayo/nekoray/issues/769](https://github.com/MatsuriDayo/nekoray/issues/769)

У человека Fedora. Закрыто со статусом “not planned”, но тут разработчик поясняет, что виновата неправильно настроенная ОС.

[https://github.com/MatsuriDayo/nekoray/issues/926](https://github.com/MatsuriDayo/nekoray/issues/926)

У человека Arch. Закрыто со статусом “not planned”. Здесь “виновато криво настроенное ядро в OS”.

Заметьте, все три issues от разных людей, сидящих на трёх разных OS Linux. С каким флагом надо собирать ядро так и не понятно 🙁 Вопрос, достойный скрининга в Яндекс!

Очевидный костыль - это запуск приложения всегда от sudo. Как делается это для классической Ubuntu 22.04:

Ярлыки приложений лежат в `/usr/share/applications/`, открываем `/usr/share/applications/nekoray.desktop` и в Exec перед sh ставим sudo. Получаем:

```
Exec=sudo sh -c "PATH=/opt/nekoray:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin /opt/nekoray/nekoray -appdata"
```

Ещё можно запускать из консоли:

```
sudo /opt/nekoray/nekoray -appdata
```

Теперь будет один запрос пароля, либо с настроенным visudo вообще без него.

Ещё меня напрягает использование beta версий sing-box в релизах. Например, в 3.23 `更新 sing-box 1.6.0-beta1`.

Из хорошего есть deb пакет. Даже для Windows нет установщика, а для debian-like есть. Также пакет есть в [AUR](https://aur.archlinux.org/packages/nekoray-bin) .