---
## Front matter
title: "Лабораторная работа № 10"
subtitle: "Расширенные настройки SMTP-сервера"
author: "Жукова София Викторовна"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: IBM Plex Serif
romanfont: IBM Plex Serif
sansfont: IBM Plex Sans
monofont: IBM Plex Mono
mathfont: STIX Two Math
mainfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
romanfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
sansfontoptions: Ligatures=Common,Ligatures=TeX,Scale=MatchLowercase,Scale=0.94
monofontoptions: Scale=MatchLowercase,Scale=0.94,FakeStretch=0.9
mathfontoptions:
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Приобретение практических навыков по конфигурированию SMTP-сервера в части
настройки аутентификации.

# Задание

1. Настройте Dovecot для работы с LMTP (см. раздел 10.4.1).
2. Настройте аутентификацию посредством SASL на SMTP-сервере (см. раздел 10.4.2).
3. Настройте работу SMTP-сервера поверх TLS (см. раздел 10.4.3).
4. Скорректируйте скрипт для Vagrant, фиксирующий действия расширенной настройки SMTP-сервера во внутреннем окружении виртуальной машины server (см.раздел 10.4.4).


# Выполнение лабораторной работы

**Настройка LMTP в Dovecote**

На виртуальной машине server войдем под  пользователем и откроем терминал. Перейдем в режим суперпользователя. В дополнительном терминале запустим мониторинг работы почтовой службы
Добавим в список протоколов, с которыми может работать Dovecot, протокол LMTP.
Для этого в файле /etc/dovecot/dovecot.conf укажем (рис. [-@fig:001]).

![Файл](image/1.png){#fig:001 width=70%}

Настроим в Dovecot сервис lmtp для связи с Postfix. Для этого в файле /etc/dovecot/conf.d/10-master.conf заменим определение сервиса lmtp на следующую запись: (рис. [-@fig:002]).

![Настроим в Dovecot сервис lmtp](image/2.png){#fig:002 width=70%}

Переопределим в Postfix с помощью postconf передачу сообщений не на прямую, а через заданный unix-сокет: (рис. [-@fig:003]).

![Переопределим](image/3.png){#fig:003 width=70%}

В файле /etc/dovecot/conf.d/10-auth.conf зададим формат имени пользователя для аутентификации в форме логина пользователя без указания домена: (рис. [-@fig:004]).

![зададим формат имени пользователя](image/4.png){#fig:004 width=70%}

Перезапустим Postfix и Dovecot и из-под учётной записи своего пользователя отправим письмо с клиента (рис. [-@fig:005]).

![отправим письмо с клиента](image/5.png){#fig:005 width=70%}

Лог почтовой службы (рис. [-@fig:006]).

![Лог почтовой службы](image/6.png){#fig:006 width=70%}

**Настройка SMTP-аутентификации**

В файле /etc/dovecot/conf.d/10-master.conf определим службу аутентификации пользователей: (рис. [-@fig:007]).

![Оопределим службу аутентификации пользователей](image/7.png){#fig:007 width=70%}


**`service auth { ... }`** - блок настройки службы аутентификации Dovecot. Она проверяет логины/пароли и отдаёт результат другим процессам через UNIX-сокеты (не по TCP).

- **`unix_listener /var/spool/postfix/private/auth {`** - создаёт сокет в приватной директории Postfix, чтобы **Postfix мог спрашивать у Dovecot проверку учётных данных** (Dovecot как SASL для Postfix).
  - **`group = postfix`** - группа-владелец сокета `postfix`.
  - **`user = postfix`** - пользователь-владелец `postfix`.
  - **`mode = 0660`** - права `rw-rw----`: читать/писать могут только владелец и группа, остальным — нельзя.
- **`unix_listener auth-userdb {`** - второй сокет, **внутренний**: через него процессы Dovecot (imap/pop3/lmtp/doveadm) получают данные о пользователе (UID, GID, home, квоты).
  - **`mode = 0600`** - права `rw-------`: доступ только у владельца.
  - **`user = dovecot`** - владелец сокета — пользователь `dovecot`.

**Смысл:** два сокета с разными правами - «наружу» для Postfix (0660, postfix) и «внутрь» для самого Dovecot (0600, dovecot). Принцип наименьших привилегий: каждый сокет открыт только тем, кому он реально нужен.

Для Postfix зададим тип аутентификации SASL для smtpd и путь к соответствующему unix-сокету: (рис. [-@fig:008]).

![Зададим](image/8.png){#fig:008 width=70%}

Настроим Postfix для приёма почты из Интернета только для обслуживаемых нашим сервером пользователей или для произвольных пользователей локальной машины (имеется в виду локальных пользователей сервера), обеспечивая тем самым запрет на использование почтового сервера в качестве SMTP relay для спам-рассылок  (рис. [-@fig:009]).

![Опции](image/9.png){#fig:009 width=70%}


**`reject_unknown_recipient_domain`**
Отклоняет запросы, когда домен получателя не существует (не имеет записи A или MX). Предотвращает приём почты для несуществующих доменов и снижает нагрузку на последующую обработку.

**`permit_mynetworks`**
Разрешает доступ клиентам из доверенных сетей (`mynetworks`). Обычно включает локальный сегмент сети или localhost - это соответствует требованию «разрешить произвольным локальным пользователям».

**`reject_non_fqdn_recipient`**
Отклоняет запросы, когда адрес получателя не соответствует формату полного доменного имени (FQDN) из RFC. Например, отклоняется `user@` без доменной части.

**`reject_unauth_destination`** ← **ключевая опция**
Отклоняет запросы, когда домен получателя не принадлежит серверу (не входит в `mydestination`, `virtual_alias_domains` и т.п.) и отправитель не прошёл аутентификацию. **Именно это предотвращает превращение сервера в открытый релей**: неаутентифицированные внешние пользователи могут отправлять почту только локальным пользователям этого сервера и не могут ретранслировать её на произвольные внешние адреса.

**`reject_unverified_recipient`**
Отклоняет запросы, когда адрес получателя не может быть подтверждён (проверка через `verify(8)` показывает, что адрес не существует или недоступен). Используется для уменьшения обратного рассеивания (backscatter) и отклонения недействительных получателей.

**`permit`**
Завершающее правило «разрешить». В Postfix ограничения проверяются по порядку, при совпадении `permit` дальнейшие проверки не выполняются. Обратите внимание: **`permit` здесь не означает разрешение всего** - до него уже сработали предыдущие правила, и до этой точки доходят только запросы, не отклонённые предыдущими правилами (например, локальные пользователи, уже обработанные `permit_mynetworks`, или легитимная почта, прошедшая проверку `reject_unauth_destination`). Если бы `permit` не было, могло бы возникнуть неопределённое поведение; его наличие обеспечивает «разрешение по умолчанию для уже прошедших проверку запросов».

На клиенте установим telnet: (рис. [-@fig:010]).

![Установка](image/10.png){#fig:010 width=70%}

На клиенте получим строку для аутентификации и подключимся на клиенте к SMTP-серверу посредством telnet(рис. [-@fig:011]).

![Аутентификация](image/11.png){#fig:011 width=70%}

**Настройка SMTP over TLS**

Настроим на сервере TLS, воспользовавшись временным сертификатом Dovecot.
Предварительно скопируем необходимые файлы сертификата и ключа из каталога
Сконфигурируем Postfix, указав пути к сертификату и ключу, а также к каталогу для хранения TLS-сессий и уровень безопасности: (рис. [-@fig:012]).

![Настройка SMTP over TLS](image/12.png){#fig:012 width=70%}

Для того чтобы запустить SMTP-сервер на 587-м порту, в файле
/etc/postfix/master.cf заменис строки (рис. [-@fig:013]).

![Исправление файла](image/13.png){#fig:013 width=70%}

Настроим межсетевой экран, разрешив работать службе smtp-submission (рис. [-@fig:014]).

![Настройка](image/14.png){#fig:014 width=70%}

**Внесение изменений в настройки внутреннего окружения виртуальной машины**

На виртуальной машине server перейдем в каталог для внесения изменений в настройки внутреннего окружения /vagrant/provision/server/. В соответствующие подкаталоги поместим конфигурационные файлы Dovecot и Postfix: (рис. [-@fig:015]).

![Поместим](image/15.png){#fig:015 width=70%}

Внесем соответствующие изменения по расширенной конфигурации SMTP-сервера в файл /vagrant/provision/server/mail.sh (рис. [-@fig:016]).

![Изменения](image/16.png){#fig:016 width=70%}

# Выводы

Мы приобрели практические навыки по конфигурированию SMTP-сервера в части настройки аутентификации.


