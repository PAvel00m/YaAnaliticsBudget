# YaAnaliticsBudget
Скрипт на сервер работающий с WSGI для прогноза бюджета на 12 месяцев по ключевым фразам в Яндекс Директе.

Для работы с таблицами необходимо полуить google_client_secret:

* Алгоритм получения описан [здесь](https://developers.google.com/sheets/api/quickstart/python)
* Переименовываем полученый credentials в google_client_secret
* Запихиваем в папку YaAnaliticsBudget\secrets

Файл конфигурация находится YaAnaliticsBudget\secrets\config.ini
* строка 1 логин Яндекс Директа
* строка 2 пароль Яндекс Директа
* строка 3 id антикапчи

Необходимо поменять значение на свое
![](https://github.com/PAvel00m/YaAnaliticsBudget/blob/master/2.png)

**Примечание: При работе Яндекс Директ выдает капчу, для ее решения необходимо иметь аккаунт на [антикапче](https://anti-captcha.com/mainpage)**

**Пример формы**

![](https://github.com/PAvel00m/YaAnaliticsBudget/blob/master/1.png)
 
Столбец А – ключевые фразы каждая с новой строки

Столбец B – регионы каждый с новой строки (доступны все регионы описанные в файле regions.json)

Столбец C – платформы. Если указано “мобильные” делает прогноз только по мобильным платформам, если не указано или что-то другое берет по умолчанию прогноз по всем.


**Примечание: Входящие данные читаются только с 1 листа (Лист1!)**








Алгоритм работы
1.	Пользователь отправляет на сервер POST запросом идентификатор таблицы в переменной t_id в скрипт pyYaAnalitics.wsgi
![](https://github.com/PAvel00m/YaAnaliticsBudget/blob/master/3.png)
 
2.	Программа считывает с первого листа из диапазона А2:С31 ключи, регионы и платформу

3.	Выводит результат прогноза по всем месяцам со строки 34 и делает сумму по каждому столбцу

