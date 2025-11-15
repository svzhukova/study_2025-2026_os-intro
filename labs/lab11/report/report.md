---
## Front matter
title: "Лабораторная работа № 11"
subtitle: "Лабораторная работа: Управление загрузкой системы"
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

Получить навыки работы с загрузчиком системы GRUB2.



# Выполнение лабораторной работы

**Модификация параметров GRUB2**

Запустите терминал и получите полномочия администратора, в файле /etc/default/grub установите параметр отображения меню загрузки в течение 10 секунд: (рис. [-@fig:001]).

![Меняем строчку](image/1.png){#fig:001 width=70%}

Сохраним изменения в файле и закроем редактор.

Запишем изменения в GRUB2, введя в командной строке (рис. [-@fig:002]).

![Введем](image/2.png){#fig:002 width=70%}

Перезагрузим систему и убедимся, что при загрузке вы видите прокрутку загрузоч-
ных сообщений.

**Устранения неполадок** 

Посмотрим список всех файлов модулей, которые загружены в настоящее время: (рис. [-@fig:003]).

![Список всех файлов модулей](image/3.png){#fig:003 width=70%}


Посмотрим задействованные переменные среды оболочки: (рис. [-@fig:004]).

![Задействованные переменные среды оболочки](image/4.png){#fig:004 width=70%}

После успешного входа в систему посмотрим список всех загруженных файлов модулей (рис. [-@fig:005]).

![Список всех загруженных файлов модулей](image/5.png){#fig:005 width=70%}

Перегрузим систему (рис. [-@fig:006]).

![Перегрузим](image/6.png){#fig:006 width=70%}

**Сброс пароля root**

Запустим компьютер. Когда отобразится меню GRUB, выберем в меню строку с текущей версией ядра системы и нажмем e , чтобы войти в режим редактора. В конце строки, загружающей ядро, введем (рис. [-@fig:007]). 

![Введем](image/7.png){#fig:007 width=70%}



Сменим пароль (рис. [-@fig:008]).

![passwd](image/8.png){#fig:008 width=70%}



**Контрольные вопросы**


# **1. Какой файл нужно изменить для общих настроек GRUB2?**

Это файл **шаблонов**, его редактируют вручную:

### **/etc/default/grub**

Все пользовательские настройки (таймаут, параметры ядра, заставка и т.д.) вносятся именно туда.



# **2. Как называется конфигурационный файл GRUB2, который применяется при загрузке?**

Файл, который реально читается при загрузке UEFI-системы:

### **/boot/efi/EFI/fedora/grub.cfg**

(в Fedora)

или

### **/boot/efi/EFI/redhat/grub.cfg**

(иногда в серверных системах)

Он **НЕ редактируется вручную** — его перегенерирует GRUB.



# **3. Какую команду выполнить, чтобы обновить конфигурацию GRUB2?**

В системе с UEFI (UTM / Mac / любой современный компьютер):

### **grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg**

или для других дистрибутивов:

### Rocky / RHEL / AlmaLinux:

```
grub2-mkconfig -o /boot/efi/EFI/rocky/grub.cfg
```

```
grub2-mkconfig -o /boot/efi/EFI/redhat/grub.cfg
```
# Выводы

Мы получили навыки работы с загрузчиком системы GRUB2.

