---
## Front matter
title: "Лабораторная работа № 13"
subtitle: "Фильтр пакетов"
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

**Управление брандмауэром с помощью firewall-cmd**


Получим полномочия администратора
Определим текущую зону по умолчанию
Определим доступные зоны 
Посмотрим службы, доступные на нашем компьютере, используя (рис. [-@fig:001]).

![Посмотрим службы](image/1.png){#fig:001 width=70%}

Определим доступные службы в текущей зоне: (рис. [-@fig:002]).

![Определим](image/2.png){#fig:002 width=70%}


Сравним результаты вывода информации при использовании команды
firewall-cmd --list-all и команды firewall-cmd --list-all --zone=public (рис. [-@fig:003]).

![Сравним результаты вывода](image/3.png){#fig:003 width=70%}


Добавим сервер VNC в конфигурацию брандмауэра
Проверим, добавился ли vnc-server в конфигурацию (рис. [-@fig:004]).

![Проверим](image/4.png){#fig:004 width=70%}


Провермс, есть ли vnc-server в конфигурации:
Обратим внимание, что служба vnc-server больше не указана. Добавим службу vnc-server ещё раз, но на этот раз сделаем её постоянной, используя команду
Проверим наличие vnc-server в конфигурации (рис. [-@fig:005]).

![Проверим](image/5.png){#fig:005 width=70%}


Перезагрузим конфигурацию firewalld и просмотрим конфигурацию времени выполнения: (рис. [-@fig:006]).


![Перезагрузим](image/6.png){#fig:006 width=70%}


Добавим в конфигурацию межсетевого экрана порт 2022 протокола TCP, затем перезагрузите конфигурацию Проверим, что порт добавлен в конфигурацию (рис. [-@fig:007]).


![Проверим](image/7.png){#fig:007 width=70%}


**Управление брандмауэром с помощью firewall-config** 

1. Откроем терминал и под учётной записью своего пользователя запустим интерфейс
Служба отсутствует, система предложила вам её установить. Также при запуске
потребовалось ввести пароль пользователя с полномочиями управления этой службой.
2. Нажмем выпадающее меню рядом с параметром Configuration . Откроем раскрывающийся список и выберем Permanent . Это позволит сделать постоянными все изменения, которые мы внесем при конфигурировании.
3. Выберем зону public и отметим службы http, https и ftp, чтобы включить их.
4. Выберем вкладку Ports и на этой вкладке нажмем Add . Введем порт 2022 и протокол udp, нажмем ОК , чтобы добавить их в список.
5. Закроем утилиту firewall-config (рис. [-@fig:008]).

![firewall-config](image/8.png){#fig:008 width=70%}


В окне терминала введем команду, обратим внимание, что изменения, которые мы только что внесли, ещё не вступили в силу. Это связано с тем, что мы настроили их как постоянные изменения, а не как изменения времени выполнения. Перегрузим конфигурацию firewall-cmd и список доступных сервисов,Мы увидим, что изменения были применены. (рис. [-@fig:009]).


![Изменения были применены](image/9.png){#fig:009 width=70%}


**Самостоятельная работа**

1. Создадим конфигурацию межсетевого экрана, которая позволяет получить доступ к следующим службам:
– telnet;
– imap;
– pop3;
– smtp.
2. Сделаем это как в командной строке (для службы telnet), так и в графическом интерфейсе (для служб imap, pop3, smtp).
3. Убедимся, что конфигурация является постоянной и будет активирована после перезагрузки компьютера. (рис. [-@fig:010]).

![Выполняем](image/10.png){#fig:010 width=70%}





# Контрольные вопросы


1. **Служба, которая должна быть запущена**: 
   Перед началом работы с менеджером конфигурации брандмауэра `firewall-config` необходимо запустить службу `firewalld`. Команда для запуска службы:
   ```bash
   sudo systemctl start firewalld
   ```

2. **Команда для добавления UDP-порта 2355**:
   ```bash
   sudo firewall-cmd --add-port=2355/udp
   ```

3. **Команда для отображения всей конфигурации брандмауэра во всех зонах**:
   ```bash
   sudo firewall-cmd --list-all-zones
   ```

4. **Команда для удаления службы vnc-server из текущей конфигурации**:
   ```bash
   sudo firewall-cmd --remove-service=vnc-server
   ```

5. **Команда для активации новой конфигурации, добавленной с опцией --permanent**:
   ```bash
   sudo firewall-cmd --reload
   ```

6. **Параметр для проверки добавления новой конфигурации**:
   ```bash
   sudo firewall-cmd --list-all
   ```

7. **Команда для добавления интерфейса eno1 в зону public**:
   ```bash
   sudo firewall-cmd --zone=public --add-interface=eno1
   ```

8. **Зона для нового интерфейса без указания**:
   Если новый интерфейс добавляется в конфигурацию брандмауэра без указания зоны, он будет добавлен в зону `drop` по умолчанию.



# Выводы

Мы приобрели навыки настройки сетевых параметров системы.
 
