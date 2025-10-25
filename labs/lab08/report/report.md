---
## Front matter
title: "Лабораторная работа № 8"
subtitle: "Лабораторная работа: Планировщики событий"
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

Целью данной работы является получение навыков работы с планировщиками событий cron и at.



# Выполнение лабораторной работы

**Планирование задач с помощью cron**

Запустиv терминал, получим полномочия администратора, Посмотрим статус демона crond: (рис. [-@fig:001]).

![Cтатус демона crond active](image/1.png){#fig:001 width=70%}


Посмотрим содержимое файла конфигурации /etc/crontab(рис. [-@fig:002]).

![Содержимое файла конфигурации](image/2.png){#fig:002 width=70%}

Посмотрим список заданий в расписании (рис. [-@fig:003]).

![Ничего не отображается, так как расписание ещё не задано.](image/3.png){#fig:003 width=70%}


Откроем файл расписания на редактирование, (crontab -e)
Команда запустит интерфейс редактора (по умолчанию используется vi). Добавим следующую строку в файл расписания (рис. [-@fig:004]).

![Добавим](image/4.png){#fig:004 width=70%}

Посмотрим список заданий в расписании (рис. [-@fig:005]).

![Появилась запись о запланированном событии](image/5.png){#fig:005 width=70%}

Не выключая систему, через некоторое время (2–3 минуты) просмотрим журнал
системных событий: (рис. [-@fig:006]).

![Журнал системных событий](image/6.png){#fig:006 width=70%}

Изменим запись в расписании crontab на следующую (рис. [-@fig:007]). 

![Изменим](image/7.png){#fig:007 width=70%}

Посмотрим список заданий в расписании: (рис. [-@fig:008]).

![Посмотрим](image/8.png){#fig:008 width=70%}

Перейдем в каталог /etc/cron.hourly и создадим в нём файл сценария с именем eachhour, откроем файл eachhour для редактирования и пропишем в нём следующий скрипт (рис. [-@fig:009]).
 
![Пропишем](image/9.png){#fig:009 width=70%}

Теперь перейдем в каталог /etc/crond.d и создадим в нём файл с расписанием
Откроем этот файл для редактирования и поместим в него следующее содержимое: (рис. [-@fig:010]).

![Файл](image/10.png){#fig:010 width=70%}


Не выключая систему, через некоторое время (2–3 часа) просмотрим журнал системных событий (рис. [-@fig:011]).

![Журнал системных событий](image/11.png){#fig:011 width=70%}

**Планирование заданий с помощью at**

Запустим терминал и получим полномочия администратора, проверим, что служба atd загружена и включена, Зададим выполнение команды logger message from at в 18:34 (рис. [-@fig:012]).

![Служба atd](image/12.png){#fig:012 width=70%}

Убедимся, что задание действительно запланировано, с помощью команды grep 'from at' /var/log/messages посмотрим, появилось ли соответствующее сообщение в лог-файле в указанное вами время. (рис. [-@fig:013]).


![Посмотрим](image/13.png){#fig:013 width=70%}


**Контрольные вопросы**


### 1. Настройка задания cron для выполнения раз в 2 недели
Для задания, которое будет выполняться раз в две недели, нужно использовать поле определяющее дни месяца, однако стандартный cron не поддерживает работу «каждые 2 недели» напрямую. Один из способов — это добавить условие в вашем скрипте для проверки, прошло ли уже 14 дней с последнего выполнения.

Пример команды для cron, которая будет выполняться в понедельник в 00:00:
```
0 0 * * 1 [ "$(date +\%s)" -eq "$(date -d 'last run' +\%s)" ] || (command && touch 'last run')
```

### 2. Задание cron для выполнения 1-го и 15-го числа в 2 часа ночи
```
0 2 1,15 * * /path/to/your/command
```
### 3. Задание cron для выполнения каждые 2 минуты каждый день
```
*/2 * * * * /path/to/your/command
```
### 4. Задание cron для выполнения 19 сентября ежегодно
```
0 0 19 9 * /path/to/your/command
```
### 5. Задание cron для выполнения каждый четверг сентября ежегодно
```
0 0 * 9 4 /path/to/your/command
```
Здесь 4 — это номер четверга для 0 0.

### 6. Назначение задания cron для пользователя alice
Чтобы назначить задание cron конкретному пользователю, используйте команду `crontab` с опцией `-u`. Пример:
```
sudo crontab -u alice -e
```
Это откроет редактор для редактирования crontab для пользователя *alice*.

### Примеры команд
Для каждого задания замените `/path/to/your/command` на команду или скрипт, который вы хотите запустить.


# Выводы

Мы приобрели практические навыки работы с планировщиками событий cron и at.

