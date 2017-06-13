VBot
======
![](http://i.imgur.com/mvTQd8T.png)
======

## Для работы бота необходим<br>Python 3.6+ или PyPy3.5<br>С версиями ниже бот не работает

![](http://i.imgur.com/jEpqC2J.gif)

## Настройка
1. Перейдите в папку с ботом
2. Установить зависимости из файла `requirements.txt`<br>
   Возможные команды для установки:<br>
   `pip3 install -r requirements.txt`<br>
   `python -m pip install -r requirements.txt`<br>
   `python3.6 -m pip install -r requirements.txt`
3. Запустите бота, чтобы он создал файл `settings.py`(после чего он выключится)<br>
   Возможные команды для запуска(из консоли, из папки с ботом):<br>
   `python3 vbot.py`<br>
   `python vbot.py`<br>
   `python3.6 vbot.py`<br>
4. В `settingsё.py` замените `TOKEN` на access_token группы или `LOGIN` и `PASSWORD` на логин и пароль аккаунта ВК соответственно. И уберите `#` перед введёнными данными <br>
   Если ввести и то и другое - бот будет работать как группа, и сможет использовать методы VK API пользователя.<br>
   Можно вводить несколько аккаунтов, но отвечать бот будет со всех без разбора, так что рекомендуется вводить только 1 группу и 1 пользователя максимум!<br>
   Без данныз пользователя некоторые плагины могут не работать! Например, !скажи не будет работать! 
5. Там же в `settings.py` вы можете ввести PROXY в указанном формате, но не гарантированно, что ВК пустит вас без подтверждения телефонного номера с этого PROXY, что бот автоматически не делает.
6. Укажите данные базы данных PostgreSQL или MySQL в DATABASE_SETTINGS в указанном формате. Создать свою БД можно на вашем сервере или, например, на [Heroku](https://devcenter.heroku.com/articles/heroku-postgresql)
7. Можете запускать бота, как в п.3. тепер ьбот должен работать!
8. Бота можно бесплатно захостить на Heroku. [Гайд](http://disonds.com/2017/03/20/python-bot-dlya-vk-na-heroku/), [Еще один гайд](https://github.com/Myzon/heroku-python-script).

Текущая версия бота: 5.0

## Смена префиксов
По умолчанию бот отзывается на префикс: `!`.
Сменить их можно в `settings.py` на 32 строке.

## Плагины
* Приветствие (плагин приветствия)
* Список плагинов (список загруженных плагинов)
* Музыка (список музыки из ваших рекомендаций в ВК)
* Случайное число (случайное число в разных диапазонах)
* Случайные мемы (берутся из паблика, указанного в плагине memes.py)
* Ближайшие дни рождения в группе (берутся из паблика, указанного в плагине birthday.py)
* Курс валют (отображение основных курсов валют)
* Список команд (список всех команд бота с описанием, как их использовать)
* Шар восьмерка (решает за вас)
* Время (показывает текущую дату и время)
* Статистика бота (показывает данные о счетчиках аккаунта)
* Послать сообщение (посылает сообщение другому пользователю, в том числе анонимное)
* Блокнот (может запоминать и вспоминать строки)
* Рассказать шутку (рассказывает случайный анекдот)
* Контроль бота (только для админов)
* Поиск видео (Ищет видео в ВК по запросу пользователя)
* Скриншот сайта (делает скриншот сайта)
* Погода (показывает погоду в Москве или указанном городе)
* Перечеркиватель (перечеркивает строку)
* Автоматическое добавление друзей (принимает входящие заявки в друзья раз в 10 секунд)
* Новости (показывает последние новости из Yandex)
* Объявление (не рассылка)(позволяет администраторам оставлять сообщение, которое могут прочитать только определённые люди)
* Переписка с ботом (пользователи могут пообщаться с ботом от ChatterBot! Работает только при USE_CHATTER = False)

## Общение с ботом (элементы чат-бот)
VBot так-же позволяет развлекать пользователей беседами.<br>
Инструкции по написанию логики бесед вы можете найти в [chat/chat.py](https://github.com/VKBots/VBot/blob/master/chat/chat.py), а так-же в настройках.<br>
Вы можете сами описание поведение бота, или воспользоваться [ChatterBot](https://github.com/gunthercox/ChatterBot).<br>
Настроить ChatterBot вы можете в [chat/chatter.py](https://github.com/VKBots/VBot/blob/master/chat/chatter.py) внизу(класс ChatterBot).

## Миграции БД
Миграции производятся с помощью файла `migrate.py` в папке `scripts`

## Примечания
* Для того, чтобы узнать ID пользователя или группы, используйте https://vk.com/linkapp
* Чтобы очистить списки администраторов, белый лист, чёрный список, используйте программу `clear_lists.py` в папке `scripts`

## Создание плагинов
В папке plugins есть пример плагина в файле example.py, отвечающий на команду `!тест`.
В нём подробно расписана структура плагина. Для примера работы plugin.data или plugin.temp_data 
вы можете посмотреть memo.py, weather.py. Для примера цикличных задач friends.py.<br>
Там есть и другие плагины, код которых можно просмотреть для понимания того, что можно сделать с помощью бота.

Каждый плагин должен иметь экземпляр класса Plugin (из plugin_system) под именем (обязательно) plugin.
Все команды, на которые подписывается плагин, должны быть в нижнем регистре.

Вот пример простого плагина:
```python
# Импортируем класс Plugin
from plugin_system import Plugin
# Создаём объект класса, через него мы будем "подписываться" на команды
plugin = Plugin('Плагин для еды')

# Использование async и await обязательно, т.к. бот асинхронный
@plugin.on_command('еда')
async def test(msg, args):
    # Отвечаем пользователю
    await msg.answer('Где еда?!')
```

Для хранения данных используется [peewee-async](https://peewee-async.readthedocs.io/en/latest/index.html).<br>
После импорта всего из database(именно таким образом)
```
from database import *
```
Вы можете использовать db, который является экземпляром peewee_async.Manager. В database.py хранятся модели бд.<br>Если данные для БД не введены, то бот будет использовать словарь для базовых функций. Подробнее: [database.py](https://github.com/VKBots/VBot/blob/master/database.py), [fake_database.py](https://github.com/VKBots/VBot/blob/master/fake_database.py).

Плагины размещаются в папке `plugins`. Если два плагина имеют одинаковые команды - они обрабатываются в обоих плагинах.<br>
Плагины могут работать со всеми методами API ВКонтакте.

## Помощь и вклад
Проект открыт, любой может отправить свой Pull request на рассмотрение! Мы обязательно изучим, обсудим и, возможно, примем изменения.

#### Связь с нами
Разработчиков этого бота можно найти в вк:
* https://vk.com/michaelkrukov
