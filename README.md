# detector()
Надеюсь название хоть немного говорит само за себя.
1. Это стандартный парсер телеграма по адресу [t.me](https://t.me/).
  Ну то есть конкретно двух каналов по игре ChatWars [ChatWarsAuction](https://t.me/ChatWarsAuction) и [chatwars3](https://t.me/chatwars3)
> Данная функция когда-то была частью нотифай бота, по факту таковой и осталась, просто теперь вынесена в отдельный скрипт, чтобы не нагружать память основного бота.
2. __Что он делает?__
   1. Первым делом при запуске проверяет доступность каналов (еще и [lot_updater](https://t.me/lot_updater)) и точки отсчета на которой он закончил.
   2. И начинает проверять на единицу выше по каналу аукциона с периодичностью где-то 0.4 секунды.
   > Почему так медленно? Ну потому что этот бот проверяет две ссылки в двух потоках с такой скоростью. Это приблизительно равно 300 запросам в минуту, на которые нужно ровняться.
   > Потому что, телеграм перестает возвращать нормальные посты, а только ошибки.
   3. Там стоит красивая схема, что если скрипт нашел пост (а раньше его не было), он почти никак его не изменяя (кроме знаков переноса на слеш а слеш поменяет меняет на его html версию), отправит это все на мой специализированный канал - [lot_updater](https://t.me/lot_updater).
   4. Но не просто отправит новым сообщением, а изменит старое, которое он проверял при запуске.
   5. И так каждый раз, с любым аукционным постом.
3. Звучит _довольно_ бесполезно. Но это не так. На том канале сидят другие боты, которые ловят сигнатуру изменившегося поста и могут уже с этим работать дальше.
4. Собственно с этими сигнатурами как раз и работает следующая функция [oldest](https://github.com/steve10live/oldest).
   > Которая тоже когда-то была частью нотифай бота, но жрала тоже много памятии была вынесена в отдельного бота, только там уже серьезно и нужна для каждого сервера отдельная.


`Ну и любопытненький факт`
Методом проб и ошибок додумался, что функций две, они абсолютно идентичные и можно было бы передавать только название сервера, но тогда я не умел передавать в _thread_ функцию переменные. Пришлось экспериментировать. Ушло где-то часа три, на то, чтобы догадаться как это работает самому, хотя мог открыть документацию и за две минуты все узнать.
С тех пор всегда перед ~~едой~~ кодингом читаю документацию, чего и вам __настоятельно__ желаю. Успехов.

04.11.2020
