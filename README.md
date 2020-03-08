Ветка Snoop Termux (Android)
===========================

## Snoop Project один из самых перспективных OSINT-инструментов по поиску никнеймов.

<img src="https://raw.githubusercontent.com/snooppr/snoop/termux/images/snoop.png" />

Snoop Project разыскивает никнеймы в публичных данных. Это самое сильное ПО с учётом
СНГ локации.

Ветка Snoop для OS GNU/Linux и Windows смотри https://github.com/snooppr/snoop

Историю смотри
https://raw.githubusercontent.com/snooppr/snoop/master/changelog.txt

**В базе** [506 сайтов](https://github.com/snooppr/snoop/blob/termux/sites.md "database"), **база расширяется**

## Установка Snoop на Android/Termux

**Примечание**: Требуемая версия python 3.6 и выше.
**Примечание**: Snoop Project стабильно работает даже на самых слабых гаджетах.

```bash
# Работа Snoop на Android-е
Войти в домашнюю папку Termux (т.е. просто открыть Termux)
$ termux-setup-storage
$ cd /data/data/com.termux/files/home #дефолтный/домашний каталог

# Клонировать репозиторий Snoop ветку Termux
# (Если флешкa FAT — она не пойдет!
#В таком случае, клонировать репозиторий только в Домашнюю дирректорию Termux)
$ git clone https://github.com/snooppr/snoop -b termux

# Войти в рабочий каталог
$ cd ~/snoop

# Установить python3 и python3-pip, если они не установлены
$ apt update && pkg upgrade && pkg install python libcrypt
#Возможно, нужно будет доставить ещё: libxml2; libxslt; и clang [Комментарий юзера]


# Установить зависимости 'requirements'
$ pip install --upgrade pip
$ python3 -m pip install -r requirements.txt
# Либо установить все зависимости из 'requirements.txt' в ручную через
$ pip3 install module


# Чтобы иметь возможность обновлять Snoop на Android/Termux
# добавьте любое 'рандомное' имя и почту [^1]:
$ git config --global user.email "you@example.com"
$ git config --global user.name "username"
$ python3 snoop.py --update y
```
**Эта версия Snoop, которая работает на Android/Termux**

## Использование

```bash
$ python3 snoop.py --help

usage: snoop.py [-h] [--donate Y] [--sort Y] [--version] [--verbose] [--csv]
                [--json] [--site] [--time] [--found-print] [--no-func]
                [--userload] [--list all] [--country] [--update Y]
                USERNAMES [USERNAMES ...]

Snoop: поиск никнейма по всем фронтам! (Version 1.1.3_rus Ветка GNU/Linux)

positional arguments:
  USERNAMES             Никнейм разыскиваемого пользователя, поддерживается
                        несколько имён

optional arguments:
  -h, --help            show this help message and exit
  --donate Y            Пожертвовать на развитие Snoop project-а
  --sort Y              Обновление/сортировка черного и белого списков (.json)
                        сайтов БД Snoop. Если вы не разработчик, не
                        используйте эту опцию
  --version, --about,-V Вывод на печать версий: Snoop; Python и Лицензии
  --verbose, -v         Во время поиска 'username' выводить на печать
                        подробную вербализацию
  --csv                 По завершению поиска 'username' сохранить файл в
                        формате таблицы 'username.CSV' с расширенным анализом
  --json , -j           Указать для поиска 'username' другую БД в формате
                        'json', например, 'example_data.json'. Если у вас нет
                        такой БД, не используйте эту опцию
  --site , -s           Указать имя сайта из БС '--list all'. Поиск 'username'
                        на одном указанном ресурсе
  --time , -t 9         Установить выделение макс.времени на ожидание ответа
                        от сервера (секунды). Влияет на продолжительность
                        поиска. Влияет на 'Timeout ошибки:'Оптимальное
                        значение при хорошем интернет соединении и нескольких
                        'упавших' сайтов = 9с. Вкл. эту опцию необходимо
                        практически всегда, чтобы избежать длительных
                        зависаний
  --found-print, -f     Выводить на печать только найденные аккаунты
  --no-func, -n         ✓Монохромный терминал, не использовать цвета в url
                        ✓Запретить открытие web browser-а
                        ✓Отключить вывод на печать для флагов стран
  --userload , -u       Указать файл со списком user-ов. Пример, 'python3
                        snoop.py -u ~/file.txt start'
  --list all            Вывод на печать БД (БС+ЧС) поддерживаемых сайтов
  --country, -c         Сортировка 'вывода на печать/запись в html'
                        результатов по странам, а не по алфавиту
  --update Y            Обновить Snoop
```

**Примеры**
```bash
# Для поиска только одного пользователя:
$ python3 snoop.py username1
# Или, например, кириллица поддерживается:
$ python3 snoop.py олеся

# Для поиска одного и более юзеров:
$ python3 snoop.py username1 username2 username3 username4

# Поиск множества юзеров — сортировка вывода результатов по странам;
# избежание зависаний на сайтах (чаще 'мёртвая зона' зависит от вашего ip-адреса);
# выводить на печать только найденные аккаунты; дополнить отчёт csv файлом;
# указать файл со списком разыскиваемых аккаунтов:
$ python3 snoop.py -с -t 9 -f --csv -u ~/file.txt start

# 'ctrl-c/z' — прервать поиск
```

Найденные учетные записи будут храниться в ~/snoop/results/*/username.{txt.csv.html}.

Если вы желаете анализировать результаты Html/CSV, то скопируйте результаты поиска из домашней папки Termux в Download, например, с помощью Total Commander.  
Откройте файл(ы) с помощью любого web-browser/office (на Android "обычно/root" нет упрощенного доступа программ к домашней папке Termux и пд.).

```bash
# Обновляйте Snoop для поддержки ПО и БД в актуальном состоянии:
$ python3 snoop.py --update Y
[^1]: Требуется установка и лёгкая "настройка" Git.
```

## Основные ошибки ложно-положительного отклика/соединения при поиске username
Cайт изменил свой ответ.  
Блокировка сервером диапазона ip-адресов клиента.  
Блокировка доступа к ресурсам при помощи РКН-а.  
Срабатывание/защита ресурса captch-ей.  
Недостаточная скорость интернет соединения EDGE/3G (желательная скорость >= 3Mbps).  
В некоторых случаях недопустимое username.  
Проблемы с openssl на стороне сервера (использование старой базы кода).  
Некоторые сайты временно недоступны, например, технические работы.

**Лицензия Snoop Project:** https://github.com/snooppr/snoop/blob/master/COPYRIGHT
