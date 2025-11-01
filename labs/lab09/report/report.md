---
## Front matter
title: "Лабораторная работа № 9"
subtitle: "Лабораторная работа: Управление SELinux"
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

Получить навыки работы с контекстом безопасности и политиками SELinux.



# Выполнение лабораторной работы

**Управление режимами SELinux**

Запустим терминал и получите полномочия администратора и просмотрим текущую информацию о состоянии SELinux (рис. [-@fig:001]).

![Cостояние SELinux](image/1.png){#fig:001 width=70%}


Посмотрим, в каком режиме работает SELinux: (рис. [-@fig:002]).

![Режим работы SELinux](image/2.png){#fig:002 width=70%}

Измените режим работы SELinux на разрешающий (Permissive): (рис. [-@fig:003]).

![Permissive](image/3.png){#fig:003 width=70%}


снова введем (рис. [-@fig:004]).

![getenforce](image/4.png){#fig:004 width=70%}

В файле /etc/sysconfig/selinux с помощью редактора установим SELINUX=disabled
Перезагрузим систему (рис. [-@fig:005]).

![SELINUX=disabled](image/5.png){#fig:005 width=70%}

Посмотрите статус SELinux: (рис. [-@fig:006]).

![Мы увидим, что SELinux теперь отключён.](image/6.png){#fig:006 width=70%}

**Использование restorecon для восстановления контекста безопасности**


1. Запустите терминал и получите полномочия администратора.
2. Посмотрите контекст безопасности файла /etc/hosts:
Мы увидим, что у файла есть метка контекста net_conf_t.
3. Скопируем файл /etc/hosts в домашний каталог:
Проверим контекст файла ~/hosts:
Поскольку копирование считается созданием нового файла, то параметр контекста
в файле ~/hosts, расположенном в домашнем каталоге, станет admin_home_t.
4. Попытаемся перезаписать существующий файл hosts из домашнего каталога в ката-
и подтвердим, что вы хотим сделать это.
5. Убедимся, что тип контекста по-прежнему установлен на admin_home_t (рис. [-@fig:007]). 

![restorecon](image/7.png){#fig:007 width=70%}

Исправим контекст безопасности
Опция -v покажет процесс изменения.
7. Убедимся, что тип контекста изменился
8. Для массового исправления контекста безопасности на файловой системе введем 
и перезагрузите систему. (рис. [-@fig:008]).

![Исправим контекст безопасности](image/8.png){#fig:008 width=70%}

**Настройка контекста безопасности для нестандартного расположения файлов веб-сервера**

1. Запустите терминал и получите полномочия администратора.
2. Установите необходимое программное обеспечение:
3. Создадим новое хранилище для файлов web-сервера:
4. Создайте файл index.html в каталоге с контентом веб-сервера:
и поместим в файл следующий текст: (рис. [-@fig:009]).

![Пропишем](image/9.png){#fig:009 width=70%}

 
В терминале под учётной записью своего пользователя при обращении к веб-серверу
в текстовом браузере lynx мы увидим веб-страницу Red Hat по умолчанию, а не содержимое только что созданного файла index.html. (рис. [-@fig:010]).

![web](image/10.png){#fig:010 width=70%}


Теперь мы получили доступ к своей пользовательской веб-странице. (рис. [-@fig:011]).

![Веб-страница](image/11.png){#fig:011 width=70%}



**Контрольные вопросы**


1. **Временное переключение SELinux в разрешающий режим**:
   ```bash
   setenforce 0
   ```

2. **Команда для получения списка всех доступных переключателей SELinux**:
   ```bash
   getsebool -a
   ```

3. **Имя пакета, необходимого для получения легко читаемых сообщений журнала SELinux**:
   ```bash
   setroubleshoot
   ```

4. **Команды для применения типа контекста `httpd_sys_content_t` к каталогу `/web`**:
   ```bash
   semanage fcontext -a -t httpd_sys_content_t '/web(/.*)?'
   restorecon -R /web
   ```

5. **Файл, который нужно изменить для полной деактивации SELinux**:
   ```bash
   /etc/selinux/config
   ```
   В этом файле необходимо изменить строку `SELINUX=enforcing` на `SELINUX=disabled`.

6. **Место, где SELinux регистрирует все свои сообщения**:
   Сообщения SELinux обычно регистрируются в файле `/var/log/audit/audit.log`.

7. **Команда для получения конкретной информации о типах контекстов для службы ftp**:
   ```bash
   seinfo --context ftp
   ```
   Или:
   ```bash
   sesearch --allow -s ftp_t
   ```

8. **Самый простой способ проверить, связано ли что-то с SELinux**:
   Используйте команду:
   ```bash
   aureport -a
   ```

# Выводы

Мы приобрели практические навыки работы с контекстом безопасности и политиками SELinux.

