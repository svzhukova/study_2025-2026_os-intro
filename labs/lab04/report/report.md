---
## Front matter
title: "Лабораторная работа № 4"
subtitle: "Лабораторная работа: Работа с программными пакетами"
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

Получить навыки работы с репозиториями и менеджерами пакетов.



# Выполнение лабораторной работы

**Работа с репозиториями**


В консоли перейдем в режим работы суперпользователя (используйте команду su -).
Перейдем в каталог /etc/yum.repos.d и изучим содержание каталога и файлов
репозиториев (рис. [-@fig:001]).

![Перейдем в каталог /etc/yum.repos.d](image/1.png){#fig:001 width=70%}

 (рис. [-@fig:002]).

![изучим содержание](image/2.png){#fig:002 width=70%}


Выведем на экран список репозиториев: (рис. [-@fig:003]).

![Выведем](image/3.png){#fig:003 width=70%}


Выведем на экран список пакетов, в названии или описании которых есть слово user (рис. [-@fig:004]).

![Выведем](image/4.png){#fig:004 width=70%}


Установим nmap, предварительно изучив информацию по имеющимся пакетам: (рис. [-@fig:005])  (рис. [-@fig:006]) (рис. [-@fig:007]).

![Установка](image/5.png){#fig:005 width=70%}


![Установка](image/6.png){#fig:006 width=70%}


![Установка](image/7.png){#fig:007 width=70%}


Удалим nmap (рис. [-@fig:008])  (рис. [-@fig:009])


![Удалим](image/8.png){#fig:008 width=70%}


![Удалим](image/9.png){#fig:009 width=70%}


Получим список имеющихся групп пакетов, затем установим группу пакетов
RPM Development Tools (рис. [-@fig:010])  (рис. [-@fig:011]) (рис. [-@fig:012])


![Получим список](image/10.png){#fig:010 width=70%}


![установим группу пакетов](image/11.png){#fig:011 width=70%}


![установим группу пакетов](image/12.png){#fig:012 width=70%}


Удалим группы пакетов RPM Development Tools (рис. [-@fig:013]).


![Удалим RPM Development Tools](image/13.png){#fig:013 width=70%}


Посмотрите историю использования команды dnf (рис. [-@fig:014]).


![Посмотрите историю использования](image/14.png){#fig:014 width=70%}



Отменим последнее, например шестое по счёту, действие(рис. [-@fig:015]).


![Отменим действие](image/15.png){#fig:015 width=70%}

**Использование rpm** 

Скачаем rpm-пакет lynx (рис. [-@fig:016]) (рис. [-@fig:017]).


![Скачаем](image/16.png){#fig:016 width=70%}


![Скачаем](image/17.png){#fig:017 width=70%}


Найдем каталог, в который был помещён пакет после загрузки(рис. [-@fig:018]).

![Найдем каталог](image/18.png){#fig:018 width=70%}

Перейдем в этот каталог и затем установите rpm-пакет (рис. [-@fig:019]).


![Перейдем и установим](image/19.png){#fig:019 width=70%}

Определим расположение исполняемого файл(рис. [-@fig:20]).


![Определим расположение](image/20.png){#fig:20 width=70%}


Используя rpm, определим по имени файла, к какому пакету принадлежит lynx(рис. [-@fig:21]).


![Определим к какому пакету принадлежит lynx](image/21.png){#fig:21 width=70%}


Получим дополнительную информацию о содержимом пакета(рис. [-@fig:22]).


![Получим дополнительную информацию](image/22.png){#fig:22 width=70%}


Получим список всех файлов в пакете (рис. [-@fig:23]).


![Получим список всех файлов в пакете](image/23.png){#fig:23 width=70%}

Выведем перечень файлов с документацией пакета  (рис. [-@fig:24]).

![Выведем перечень файлов](image/24.png){#fig:24 width=70%}

Посмотрим файлы документации, применив команду man lynx(рис. [-@fig:25]).


![Посмотрим файлы документации](image/25.png){#fig:25 width=70%}


Выведем на экран перечень и месторасположение конфигурационных файлов пакета(рис. [-@fig:26]).


![Выведем](image/26.png){#fig:26 width=70%}



Выведем на экран расположение и содержание скриптов, выполняемых при установке
пакета(рис. [-@fig:27]).


![Выведем на экран](image/27.png){#fig:27 width=70%}


В отдельном терминале под своей учётной записью запустим текстовый браузер lynx,
чтобы проверить корректность установки пакета(рис. [-@fig:28]).


![Все корректно](image/28.png){#fig:28 width=70%}

Вернемся в терминал с учётной записью root и удалим пакет(рис. [-@fig:29]).


![удалим пакет](image/29.png){#fig:29 width=70%}

Установим пакет dnsmasq и определим расположение исполняемого файла (рис. [-@fig:30]).

![Установим](image/30.png){#fig:30 width=70%}

Определим по имени файла, к какому пакету принадлежит dnsmasq (рис. [-@fig:31]).

![Посмотрим файлы документации](image/31.png){#fig:31 width=70%}


Получим дополнительную информацию о содержимом пакета (рис. [-@fig:32]).

![Получим дополнительную информацию](image/32.png){#fig:32 width=70%}

Получим список всех файлов в пакете (рис. [-@fig:33]).

![Получим список всех файлов](image/33.png){#fig:33 width=70%}

Выведем перечень файлов с документацией пакета (рис. [-@fig:34]).


![Выведем перечень файлов](image/34.png){#fig:34 width=70%}


Посмотрите файлы документации, применив команду man dnsmasq (рис. [-@fig:35]).

![Посмотрите файлы документации](image/35.png){#fig:35 width=70%}

Выведем на экран расположение и содержание скриптов, выполняемых при установке
пакета(рис. [-@fig:36]).

![Выведем](image/36.png){#fig:36 width=70%}


Вернемся в терминал с учётной записью root и удалим пакет (рис. [-@fig:37]).

![Уудалим](image/37.png){#fig:37 width=70%}

**Контрольные вопросы**


1. **Чтобы искать пакет RPM, содержащий файл `useradd`, используйте команду:**
   ```bash
   rpm -qf $(which useradd)
   ```
   Эта команда возвращает имя пакета, которому принадлежит файл `useradd`.

2. **Чтобы показать имя группы DNF, которая содержит инструменты безопасности, и отобразить ее содержимое, используйте следующие команды:**
   ```bash
   dnf group list
   ```
   Затем найдите группу, содержащую инструменты безопасности, и используйте:
   ```bash
   dnf group info <имя_группы>
   ```

3. **Чтобы установить RPM, загруженный из Интернета и не находящийся в репозиториях, используйте команду:**
   ```bash
   rpm -ivh <путь_к_файлу.rpm>
   ```

4. **Для проверки, что пакет RPM не содержит опасного кода сценария, можно использовать команду:**
   ```bash
   rpm --checksig <путь_к_файлу.rpm>
   ```
   Это проверяет цифровую подпись пакета.

5. **Чтобы показать всю документацию в RPM, используйте команду:**
   ```bash
   rpm -qd <имя_пакета>
   ```
   Эта команда выводит путь к документации, связанной с указанным пакетом.

6. **Чтобы узнать, какому пакету RPM принадлежит файл, используйте команду:**
   ```bash
   rpm -qf <путь_к_файлу>
   ```

Эти команды помогут вам выполнять различные операции с пакетами RPM и DNF.


# Выводы

Мы получили навыки работы с репозиториями и менеджерами пакетов.

