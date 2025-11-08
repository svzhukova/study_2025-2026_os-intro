---
## Front matter
title: "Лабораторная работа № 10"
subtitle: "Лабораторная работа: Основы работы с модулями ядра операционной системы"
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

Получить навыки работы с утилитами управления модулями ядра операционной системы.



# Выполнение лабораторной работы

**Управление модулями ядра из командной строки**

Запустим терминал и получим полномочия администратора, посмотритм, какие устройства имеются в нашей системе и какие модули ядра с ними связаны (рис. [-@fig:001]).

![Устройства в нашей системе и модули ядра](image/1.png){#fig:001 width=70%}


Посмотрим, какие модули ядра загружены: (рис. [-@fig:002]).

![Посмотрим](image/2.png){#fig:002 width=70%}

Загрузим модуль ядра ext4 и убедимся, что модуль загружен, посмотрев список загруженных модулей (рис. [-@fig:003]).

![Модуль ядра ext4](image/3.png){#fig:003 width=70%}


Посмотрим информацию о модуле ядра ext4 (рис. [-@fig:004]).

![Посмотрим](image/4.png){#fig:004 width=70%}

Попробуем выгрузить модуль ядра ext4 (рис. [-@fig:005]).

![Попробуем выгрузить](image/5.png){#fig:005 width=70%}

**Загрузка модулей ядра с параметрами**

Запустите терминал и получите полномочия администратора. Загрузим модуль ядра bluetooth (рис. [-@fig:006]).

![Модуль ядра bluetooth](image/6.png){#fig:006 width=70%}

Посмотрим список модулей ядра, отвечающих за работу с Bluetooth и информацию о модуле bluetooth: (рис. [-@fig:007]). 

![Посмотрим](image/7.png){#fig:007 width=70%}

Выгрузим модуль ядра bluetooth (рис. [-@fig:008]).

![Выгрузим модуль ядра bluetooth ](image/8.png){#fig:008 width=70%}

**Обновление ядра системы**

Запустим терминал и получим полномочия администратора, посмотрим версию ядра, используемую в операционной системе и выведем на экран список пакетов, относящихся к ядру операционной системы (рис. [-@fig:009]).

![Выполним](image/9.png){#fig:009 width=70%}

 
Обновим систему, чтобы убедиться, что все существующие пакеты обновлены, так
как это важно при установке/обновлении ядер Linux и избежания конфликтов и обновим ядро операционной системы, а затем саму операционную систему (рис. [-@fig:010]).

![Обновим](image/10.png){#fig:010 width=70%}


Перегрузим систему, при загрузке выберем новое ядро. Посмотрим версию ядра, используемую в операционной системы: (рис. [-@fig:011]).

![Версия ядра](image/11.png){#fig:011 width=70%}



**Контрольные вопросы**


1. **Команда для проверки текущей версии ядра:**  
   Чтобы узнать текущую версию ядра, используйте команду:
   ```bash
   uname -r
   ```

2. **Подробная информация о текущей версии ядра:**  
   Для более детальной информации о текущем ядре используйте команду:
   ```bash
   uname -a
   ```
   Эта команда отобразит информацию о системе, включая имя хоста, версию ядра, дату сборки и архитектуру.

3. **Список загруженных модулей ядра:**  
   Чтобы увидеть список загруженных модулей, используйте команду:
   ```bash
   lsmod
   ```

4. **Определение параметров модуля ядра:**  
   Для определения параметров модуля ядра, используйте команду:
   ```bash
   modinfo <имя_модуля>
   ```
   Замените `<имя_модуля>` на название модуля, информацию о котором вы хотите получить.

5. **Выгрузка модуля ядра:**  
   Чтобы выгрузить модуль ядра, используйте команду:
   ```bash
   rmmod <имя_модуля>
   ```

6. **Ошибки при выгрузке модуля ядра:**  
   Если вы получаете сообщение об ошибке при попытке выгрузить модуль, у вас могут быть следующие варианты:
   - Убедитесь, что модуль не используется (например, не занят каким-либо процессом).
   - Используйте `modprobe -r <имя_модуля>` вместо `rmmod`, чтобы автоматически выгрузить все зависимые модули.

7. **Определение поддерживаемых параметров модуля ядра:**  
   Чтобы определить, какие параметры модуля ядра поддерживаются, снова используйте команду:
   ```bash
   modinfo <имя_модуля>
   ```
   Подходящие параметры будут перечислены под заголовком, обычно начинающимся с "parm:". 

8. **Установка новой версии ядра:**  
   Установка новой версии ядра может различаться в зависимости от дистрибутива, но общая процедура выглядит следующим образом:
   - Для Ubuntu или Debian:
     ```bash
     sudo apt update
     sudo apt install linux-image-<версия>
     ```
   - Для CentOS или Fedora:
     ```bash
     sudo dnf install kernel-<версия>
     ```

# Выводы

Мы получили навыки работы с утилитами управления модулями ядра операционной системы.

