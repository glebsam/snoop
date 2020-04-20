Ветка Termux (Snoop Android)
===========================

<img src="https://raw.githubusercontent.com/snooppr/snoop/termux/images/snoop.png" />

## Install Snoop for Android/Termux

**Примечание**: Требуемая версия python 3.7 и выше.
**Примечание**: Snoop Project стабильно работает даже на самых слабых гаджетах.  

# Инсталляция
Установить [Termux](https://play.google.com/store/apps/details?id=com.termux&hl=en "Google Play")  
```
# Войти в домашнюю папку Termux (т.е. просто открыть Termux)
$ termux-setup-storage
$ ls #/data/data/com.termux/files/home дефолтный/домашний каталог

# Установить python3 и зависимости
# Примечание: установка продолжительная по времени
$ apt update && pkg upgrade && pkg install python libcrypt libxml2 libxslt git
$ pip install --upgrade pip

# Клонировать репозиторий Snoop и перейти в ветку Snoop/Termux
$ git clone https://github.com/snooppr/snoop -b termux
# (Если флешкa FAT (ни ext4), в таком случае,
# клонировать репозиторий только в ДОМАШНЮЮ директорию Termux)

# Войти в рабочий каталог Snoop
$ cd ~/snoop
# Установить зависимости 'requirements'
$ python3 -m pip install -r requirements.txt


# Дополнение для устаревших гаджетов (Android 6)
# Примечание на современных гаджетах пакеты уже предустановлены и настроены
# добавьте любое 'рандомное' имя и почту [^1]:
$ git config --global user.email "you@example.com"
$ git config --global user.name "username"
# Установите coreutils
$ pkg install coreutils
```
**Эта версия Snoop, которая работает на Android/Termux**

## Using
```
$ python3 snoop.py --help

usage: snoop.py [-h] [--donate Y] [--sort Y] [--version] [--verbose] [--json]
                [--site] [--time] [--found-print] [--no-func] [--userload]
                [--list all] [--country] [--update Y]
                USERNAMES [USERNAMES ...]

Snoop: поиск никнейма по всем фронтам! (Version 1.1.8_rus Ветка Snoop Android)

positional arguments:
  USERNAMES             Никнейм разыскиваемого пользователя, поддерживается
                        несколько имён

optional arguments:
  -h, --help            show this help message and exit
  --donate Y            Пожертвовать на развитие Snoop project-а
  --sort Y              Обновление/сортировка черного и белого списков (.json)
                        сайтов БД Snoop. Если вы не разработчик, не
                        используйте эту опцию
  --version, --about,-V Вывод на печать версий: OS; Snoop; Python и Лицензии
  --verbose, -v         Во время поиска 'username' выводить на печать
                        подробную вербализацию
  --json , -j           Указать для поиска 'username' другую БД в формате
                        'json', например, 'example_data.json'. Если у вас нет
                        такой БД, не используйте эту опцию
  --site , -s           Указать имя сайта из БС '--list all'. Поиск 'username'
                        на одном указанном ресурсе
  --time , -t 9         Установить выделение макс.времени на ожидание ответа
                        от сервера (секунды). Влияет на продолжительность
                        поиска. Влияет на 'Timeout ошибки:'Оптимальное
                        значение при хорошем интернет соединении = 9с.
                        Вкл. эту опцию необходимо практически
                        всегда, чтобы избежать длительных зависаний при
                        Internet Censorship
  --found-print, -f     Выводить на печать только найденные аккаунты
  --no-func, -n         ✓Монохромный терминал, не использовать цвета в url
                        ✓Запретить открытие web browser-а
                        ✓Отключить вывод на печать флагов стран
  --userload , -u       Указать файл со списком user-ов. Пример, 'python3
                        snoop.py -u ~/file.txt start'
  --list all            Вывести на печать информацию о базе данных Snoop
  --country, -c         Сортировка 'вывода на печать/запись_результатов'
                        по странам, а не по алфавиту
  --update Y            Обновить Snoop
```

**Example**
```
# Для поиска только одного пользователя:
$ python3 snoop.py username1
# Или, например, кириллица поддерживается:
$ python3 snoop.py олеся
# Для поиска имени, содержащего пробел:
$ python3 snoop.py "ivan ivanov"
$ python3 snoop.py ivan_ivanov

# Для поиска одного и более юзеров:
$ python3 snoop.py username1 username2 username3 username4

# Поиск множества юзеров — сортировка вывода результатов по странам;
# избежание зависаний на сайтах (чаще 'мёртвая зона' зависит от вашего ip-адреса);
# выводить на печать только найденные аккаунты;
# указать файл со списком разыскиваемых аккаунтов:
$ python3 snoop.py -с -t 9 -f -u ~/file.txt start

# 'ctrl-c/z' — прервать поиск
```
Найденные учетные записи будут храниться в ~/snoop/results/*/username.{txt.csv.html}.

Если вы желаете анализировать результаты Html/CSV, то скопируйте результаты поиска из домашней папки Termux в Download, например, с помощью Total Commander.  
Откройте файл(ы) с помощью любого web-browser/office (на Android "обычно/root" нет упрощенного доступа программ к домашней папке Termux и пд.).  

Уничтожить **все** результаты поиска — удалить каталог '~/snoop/results'.
```
# Обновляйте Snoop для поддержки ПО и БД в актуальном состоянии:
$ python3 snoop.py --update Y
[^1]: Требуется установка и лёгкая "настройка" Git (Android 6).
```

<img src="https://raw.githubusercontent.com/snooppr/snoop/termux/images/snoop_run.png" />
