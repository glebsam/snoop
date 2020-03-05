Ветка Snoop Termux (Android)
===========================

## Snoop Project один из самых перспективных OSINT-инструментов по поиску никнеймов.

<img src="https://raw.githubusercontent.com/snooppr/snoop/termux/images/snoop.png" />

Snoop Project разыскивает никнеймы в публичных данных. Это самое сильное ПО с учётом
СНГ локации.


Ветка Snoop GNU/Linux
смотри 
https://github.com/snooppr/snoop

Историю смотри
https://raw.githubusercontent.com/snooppr/snoop/master/changelog.txt

**В базе 506 сайтов, база расширяется**

## Установка Snoop на Android/Termux

**Примечание**: Требуемая версия python 3.6 и выше.

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
$ git config --global user.email "you@example.com"
$ git config --global user.name "username"
$ python3 snoop.py --update y
# E-mail и username можно указывать любое/выдуманное (для обновления Snoop этого достаточно).
```
**Эта урезанная версия Project Snoop, которая работает на Android/Termux**

## Использование

```bash
$ python3 snoop.py --help

usage: snoop.py [-h] [--donate Y] [--sort Y] [--version] [--verbose] [--csv]
                [--json] [--site] [--time] [--found-print] [--no-func]
                [--list all] [--country] [--update Y]
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
  --version, --about, -V
                        Вывод на печать версий: Snoop; Python и Лицензии
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
  --list all            Вывод на печать БД (БС+ЧС) поддерживаемых сайтов
  --country, -c         Сортировка 'вывода на печать/запись в html'
                        результатов по странам, а не по алфавиту
  --update Y            Обновить Snoop
```

Для поиска только одного пользователя::
```bash
$ python3 snoop.py username1
# Кириллица поддерживается, например,
$ python3 snoop.py олеся
```

Для поиска одного и более юзеров:
```bash
$ python3 snoop.py username1 username2 username3
# 'ctrl-c/z' — прервать поиск 
```

Найденные учетные записи будут храниться в ~/snoop/results/*/username.{txt.csv.html}.
Если вы желаете работать с Html, то скопируйте результаты поиска в html из домашней папки 
в Download, и откройте файл с помощью любого браузера (на Android "обычно" нет доступа
браузеров к домашней папке Termux).

Обновляйте Snoop для поддержки ПО и БД в актуальном состоянии:
```bash
$ python3 snoop.py --update Y 
# Требуется установка и лёгкая "настройка" Git.
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

**Лицензия Snoop Project** 
https://github.com/snooppr/snoop/blob/master/COPYRIGHT
