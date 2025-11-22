---
## Front matter
title: "Лабораторная работа № 12"
subtitle: "Настройки сети в Linux."
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

Получить навыки настройки сетевых параметров системы.



# Выполнение лабораторной работы

**Проверка конфигурации сети**


Получите полномочия администратора

Выведем на экран информацию о существующих сетевых подключениях, а также статистику о количестве отправленных пакетов и связанных с ними сообщениях об ошибках: (рис. [-@fig:001]).

![Информация о существующих сетевых подключениях](image/1.png){#fig:001 width=70%}

Выведите на экран информацию о текущих маршрутах (рис. [-@fig:002]).

![Текущие маршруты](image/2.png){#fig:002 width=70%}


Выведем на экран информацию о текущих назначениях адресов для сетевых интерфейсов на устройстве (рис. [-@fig:003]).

![Текущие назначения адресов для сетевых интерфейсов на устройстве](image/3.png){#fig:003 width=70%}


Используем команду ping для проверки правильности подключения к Интернету. (рис. [-@fig:004]).

![Подключение к Интернету](image/4.png){#fig:004 width=70%}


Добавим дополнительный адрес к нашему интерфейсу (рис. [-@fig:005]).

![Добавим](image/5.png){#fig:005 width=70%}


Проверим, что адрес добавился: (рис. [-@fig:006]).


![Добавился](image/6.png){#fig:006 width=70%}


Сравним вывод информации от утилиты ip и от команды ifconfig (рис. [-@fig:007]).


![Сравним](image/7.png){#fig:007 width=70%}


**Управление сетевыми подключениями с помощью nmcli** 

Получим полномочия администратора. Выведем на экран информацию о текущих соединениях (рис. [-@fig:008]).

![Текущие соединения](image/8.png){#fig:008 width=70%}


Добавим Ethernet-соединение с именем dhcp к интерфейсу: (рис. [-@fig:009]).


![Добавим Ethernet-соединение](image/9.png){#fig:009 width=70%}


Добавим к этому же интерфейсу Ethernet-соединение с именем static, статическим IPv4-адресом адаптера и статическим адресом шлюза (рис. [-@fig:010]).

![Добавим](image/10.png){#fig:010 width=70%}


Выведем информацию о текущих соединениях (рис. [-@fig:011]).

![Выведем информацию](image/11.png){#fig:011 width=70%}


Переключимся статическое соединение (рис. [-@fig:012]).

![Переключимся на статическое соединение](image/12.png){#fig:012 width=70%}


Вернемся к соединению dhcp (рис. [-@fig:013]).

![Вернемся к соединению dhcp](image/13.png){#fig:013 width=70%}


Проверим успешность переключения при помощи nmcli connection show и ip addr (рис. [-@fig:014]).

![Проверим](image/14.png){#fig:014 width=70%}

**Изменение параметров соединения с помощью nmcli**

Отключим автоподключение статического соединения:
Добавим DNS-сервер в статическое соединение:
Изменим IP-адрес статического соединения:
Добавим другой IP-адрес для статического соединения:
После изменения свойств соединения активируем его:
Проверим успешность переключения при помощи nmcli con show и ip addr.
Используя nmtui, посмотрим настройки сети на устройстве.
Посмотрим настройки сетевых соединений в графическом интерфейсе операционной
системы.
Переключимся на первоначальное сетевое соединение (рис. [-@fig:015]).

![Выполняем](image/15.png){#fig:015 width=70%}




# Контрольные вопросы

1. **Команда для отображения только статуса соединения**: 
   ```bash
   nmcli connection show --active
   ```
   Эта команда покажет активные подключения, не отображая IP-адреса.

2. **Служба, управляющая сетью в ОС типа RHEL**: 
   **NetworkManager** – это основная служба для управления сетевыми соединениями в системах RHEL.

3. **Файл, содержащий имя узла (устройства) в ОС типа RHEL**: 
   Имя узла хранится в файле `/etc/hostname`.

4. **Команда для задания имени узла (устройства)**: 
   ```bash
   hostnamectl set-hostname имя_узла
   ```
   Эта команда задает новое имя узла.

5. **Конфигурационный файл для включения разрешения имён для конкретного IP-адреса**: 
   Обычно изменения вносятся в файл `/etc/hosts`.

6. **Команда, показывающая текущую конфигурацию маршрутизации**: 
   ```bash
   ip route show
   ```
   Или можно использовать:
   ```bash
   route -n
   ```

7. **Проверка текущего статуса службы NetworkManager**: 
   ```bash
   systemctl status NetworkManager
   ```

8. **Команда для изменения текущего IP-адреса и шлюза по умолчанию**: 
   Для изменения адреса можно использовать:
   ```bash
   nmcli connection modify <имя_подключения> ipv4.addresses <новый_IP> ipv4.gateway <шлюз> ipv4.method manual
   ```
   После этого примените изменения:
   ```bash
   nmcli connection up <имя_подключения>
   ```


# Выводы

Мы приобрели навыки настройки сетевых параметров системы.
 
