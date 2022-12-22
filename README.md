# Portfolio QA Engineer 
В портфолио собраны проекты, выполненные во время обучения по специальности [Инженер по тестированию](https://practicum.yandex.ru/qa-engineer/) в Яндекс.Практикуме.

Проектирование тестов
        Тест-анализ | Ассоциативные карты | Блок-схемы
        Тест-дизайн | Классы эквивалентности | Граничные значения
        Тестовая документация | Чек-листы | Тест-кейсы

Тестирование веб-приложений
        Пользовательский интерфейс | Формы | DevTools | Charles
        Таблицы принятия решений | Парное тестирование | Баг-репорты

Тестирование мобильных приложений
        Матрица устройств | Эмуляторы | Android Studio

Тестирование API
        REST API | JSON | Postman

Тестирование баз данных
        Консоль | SQL | PostgreSQL

Основы автоматизации тестирования
        JavaScript | NodeJS | Puppeteer
        
## Проектирование тестов

### Задание 1
1. Визуализируй требования

Проанализируй требования к сервису Яндекс.Маршруты и нарисуй mindmap.

2. Выдели классы эквивалентности и граничные значения

Проверь: «Время начала поездки», «Откуда», «Куда».

Выдели объекты тестирования.
Определи классы эквивалентности. Укажи тип ограничений: диапазон или набор значений.
Определи граничные значения каждого класса, если применимо.
Выбери тестовые значения, которые проверят каждый класс; и границы, если они есть.
Не забудь проверить негативные сценарии.
<details><summary>Требования к сервису Яндекс.Маршруты</summary>

******

Яндекс.Маршруты — сервис, который строит маршруты для транспорта разных видов. Рассчитывает время и стоимость поездки.

**Интерфейс**

В интерфейсе есть поля «Время начала поездки», «Откуда», «Куда». Переключатели режимов маршрута: оптимальный, быстрый и свой, а также переключатели видов транспорта: свой автомобиль, каршеринг, такси, самокат, велосипед и пешком.

Пользователь вводит время отправления. Чтобы построить маршрут, нужно ввести улицу и номер дома в поля «Откуда» и «Куда». В начале и конце адреса могут быть пробелы: они допустимы, но при снятии фокуса система удалит их.

**Описание работы интерфейса**

В стартовом состоянии поля «Время начала поездки», «Откуда» и «Куда» пустые. Режимы маршрутов «Оптимальный», «Быстрый и «Свой» не выбраны; панель переключения видов транспорта неактивна.

**Логика работы полей «Откуда» и «Куда»**

Если поля адреса заполнены корректно, на карте отображаются точки А и В. Если поле «Откуда» заполнено некорректно, точка А не отображается. Если поле «Куда» заполнено некорректно, точка В не отображается. При некорректном значении поле подсвечивается красным; появляется сообщение об ошибке.

Примеры тестовых адресов есть в таблице.

**Режим «Оптимальный» и «Быстрый»**

Если выбрать режим «Оптимальный» или «Быстрый», система автоматически назначит вид транспорта; построится маршрут; отобразится время и стоимость поездки. Выбрать транспорт в этих режимах нельзя — панель видов транспорта неактивна.

**Режим «Свой»**

Если выбрать режим «Свой», панель видов транспорта активна — можно переключать. Под каждый вид транспорта строится маршрут; рассчитывается время и стоимость поездки.

Если сменить вид транспорта или поменять значение в любом поле, маршрут перестроится; время и стоимость поездки пересчитается.

**Ограничения**

| Элементы системы    | Требования         |         
| -------------           |:------------------ | 
| Поле ввода часов        | Формат 24 часа. Нули перед однозначным числом обязательны. Корректны только целые числа от 0 до 23 включительно. При некорректном вводе подсвечивается красным, ошибка «Вы ввели некорректное время».| 
| Поле ввода минут        | Только целые числа. Нули перед однозначным числом обязательны. При некорректном вводе подсвечивается красным, ошибка «Вы ввели некорректное время».| 
| Поле ввода адреса       | Только русские буквы, цифры, пробел, тире, точка, запятая. Длина не более 50 символов. Пробелы до и после адреса удаляются при снятии фокуса. При некорректном вводе подсвечивается красным, ошибка «Вы ввели некорректный адрес». |  
| Переключатели режима    | Оптимальный, Быстрый и Свой. Состояние каждого переключателя — активен, выбран.  |
| Переключатели видов транспорта   | Пешком, самокат, велосипед, каршеринг, такси, собственный автомобиль. Состояние каждого переключателя — активен, неактивен, выбран.  |

**Макеты**

![image](https://user-images.githubusercontent.com/115216040/208859806-ecf4f01c-8a40-4383-901b-eb735727c6d2.png)

![image](https://user-images.githubusercontent.com/115216040/208859898-d2149905-f7e2-4c79-b4b6-c1afe180d61a.png)

**Логика расчета**

Система получает данные о начале поездки, точке А и точке В. После этого рассчитывает продолжительность и стоимость поездки по определённому алгоритму.

![image](https://user-images.githubusercontent.com/115216040/208860045-f5f66ebe-f361-4908-8838-422f0658fbea.png)

Расстояние, скорость и стоимость за минуту или километр можно получить из таблиц. Этих данных достаточно, чтобы рассчитать время и стоимость поездки для каждого вида транспорта.

|Вид транспорта	 |Как расчитать время	|Стоимость на км|
|:---------------|:-------------------|:-----------------|
|Пешком	         |Средняя скорость 4 км/ч	|0 р / км|
|Шеринг самокатов	|Средняя скорость	|10 км/ч|
|Шеринг велосипедов|	Средняя скорость|	12 км/ч|
|Каршеринг| см. Таблицу «Средняя скорость автомобиля»	|9 р / мин|
|Такси| см. Таблицу «Средняя скорость такси»|	11 р / мин|
|Собственное авто|	см. Таблицу «Средняя скорость автомобиля»| 20 р / км|

Средняя скорость автомобиля

|Время суток	|Средняя скорость автомобиля|
|:------------|:--------------------------|
|00:01-08:00| 45 км/ч|
|08:01-12:00|	30 км/ч|
|12:01-18:00|	40 км/ч|
|18:01-22:00|	25 км/ч|
|22:01-00:00|	45 км/ч|

Средняя скорость такси с учётом движения по выделенным полосам

|Время суток	|Средняя скорость такси|
|:------------|:---------------------|
|00:01-08:00	|50 км/ч|
|08:01-12:00	|35 км/ч|
|12:01-18:00	|42 км/ч|
|18:01-22:00	|30 км/ч|
|22:01-00:00	|50 км/ч|

Матрица расстояний между адресами для автомобильных дорог, в километрах

|Адрес|	Усачева, 3	|Комсомольский проспект, 18	|Зубовский бульвар, 37	|М. Пироговская, 25	|Хамовнический Вал, 34	|Фрунзенская набережная, 46	|3-я Фрунзенская улица, 12|
|:----|:------------|:--------------------------|:----------------------|:------------------|:----------------------|:--------------------------|:-----------------------|
|Усачева, 3|	0|	1,4|	1,5|	0,89|	2,6|	2,6|	2,6|
|Комсомольский проспект, 18|	1,4|	0	|2,9|	2,3|	2,3|	2,3|	2,3|
|Зубовский бульвар, 37|	1,4|	1,5|	0|	1,9|	3,8|	3|	3,3|
|М. Пироговская, 25|	1,5|	3|	2,4|	0|	1,2|	3,4|	2,3|
|Хамовнический Вал, 34|	1,5|	3,7|	3,7|	1,2|	0|	1,7|	1,7|
|Фрунзенская набережная, 46|	3,2|	3,9|	4,7|	2,7|	1,7|	0|	2,2|
|3-я Фрунзенская улица, 12|	1,4|	2,4|	3,5|	2,3|	1,4|	1,3|	0|

Матрица расстояний между адресами для пешеходов, в километрах

|Адрес|	Усачева, 3	|Комсомольский проспект, 18	|Зубовский бульвар, 37	|М. Пироговская, 25	|Хамовнический Вал, 34	|Фрунзенская набережная, 46	|3-я Фрунзенская улица, 12|
|:----|:------------|:--------------------------|:----------------------|:------------------|:----------------------|:--------------------------|:-----------------------|
|Усачева, 3|	0|	0,96|	1,4|	0,91|	1,4|	1,7|	1,1|
|Комсомольский проспект, 18|	1|	0	|1,3|	1,9|	2|	1,7|	1,2|
|Зубовский бульвар, 37|	1,4|	1,3|	0|	1,9|	2,7|	2,7|	2,3|
|М. Пироговская, 25|	0,91|	1,9|	1,9|	0|	0,75|	1,5|	1,2|
|Хамовнический Вал, 34|	1,4|	2|	2,7|	0,75|	0|	1,4|	1,2|
|Фрунзенская набережная, 46|	1,7|	1,7|	2,7|	1,5|	1,4|	0|	0,57|
|3-я Фрунзенская улица, 12|	1,1|	1,2|	2,3|	1,2|	1,2|	0,57|	0|

Обрати внимание: для подсчёта времени и стоимости маршрута тебе доступны таблицы со скоростью движения разных видов транспорта. Они показывают скорость движения автомобиля в разное время суток. Если ты берёшь такие тестовые значения, что поездка захватывает несколько временных интервалов, алгоритм выбирает скорость автомобиля из того диапазона, в котором поездка началась.

![image](https://user-images.githubusercontent.com/115216040/208866691-a473a31a-95e2-409d-9e6b-7e5d8ba9f0fe.png)

***
</details>

### Решение

**1. Ассоциативная карта :white_check_mark:**

[Ассоциативная карта в высоком разрешении](https://miro.com/app/board/uXjVPPRjZYw=/?share_link_id=798311942070)

**2. Классы эквивалентности и граничные значения :white_check_mark:** 

<details><summary>Поле ввода часов</summary>

**************

Вводимые значения 

| Название класса       | Границы               | Тестовые данные внутри класса| Тестовые данные на границах|
| :---------------------|:----------------------|:-----------------------------|:---------------------------|
| Целые числа от 0 до 9 | 0, 9                  |5                             | 0 <br/> 9 <br/> -1 <br/> 1 <br/> 8 <br/> 10|
| Целые числа от 10 до 23| 10, 23               |16                            |~~10~~ <br/> 23 <br/> ~~9~~ <br/> 11 <br/> 22 <br/> ~~24~~  |
| Целые числа от 24     | 24                    |57                            |24 <br/> ~~23~~ <br/> 25    |

Длина поля 

| Название класса       | Границы               | Тестовые данные внутри класса| Тестовые данные на границах|
| :---------------------|:----------------------|:-----------------------------|:---------------------------|
| 0  символов           |                       |пустой ввод                   | ~~0 символов - пустой ввод~~ <br/> ~~1 символ - 5~~|
| 1-2 символа           | 1, 2                   |~~2 символа - 15~~                | ~~0 символов - пустой ввод~~ <br/> ~~1 символ - 9~~ <br/> ~~2 символа - 15~~ <br/> ~~3 символа -123~~|
| 3 и более символов    | 3                     |25 символов - 1234567891234567891234567|3 символа -123 <br/> ~~2 символа - 15~~ <br/> 4 символа - 1234|

Обязательность заполнения

| Название класса       | Границы               | Тестовые данные внутри класса| Тестовые данные на границах|
| :---------------------|:----------------------|:-----------------------------|:---------------------------|
| Поле заполнено        |                       |~~16~~                            |                            |
| Поле не заполнено     |                       |~~пустой ввод~~                   |                            |

Негативные проверки

| Название класса       | Тестовые данные внутри класса| 
| :---------------------|:-----------------------------|
| Спец.символы          |@                             |                            
| Буквы                 |два                           |                            
| Дробные числа с запятой|1,5                            |                            
| Дробные числа с точкой |2.2                            |                          
| Дробные числа через /|1/6                           |      
| Отрицательные числа|~~-1~~                          |      


~~Зачёркнутые~~ значения - оптимизация проверок
</details>

<details><summary>Поле ввода минут</summary>

**************

Вводимые значения 

| Название класса       | Границы               | Тестовые данные внутри класса| Тестовые данные на границах|
| :---------------------|:----------------------|:-----------------------------|:---------------------------|
| Целые числа от 0 до 9 | 0, 9                  |5                             | 0 <br/> 9 <br/> -1 <br/> 1 <br/> 8 <br/> 10|
| Целые числа от 10 до 59| 10, 59               |45                           |~~10~~ <br/> 59 <br/> ~~9~~ <br/> 11 <br/> 58 <br/> ~~60~~  |
| Целые числа от 60     | 60                    |85                          |60 <br/> ~~59~~ <br/> 61    |

Длина поля 

| Название класса       | Границы               | Тестовые данные внутри класса| Тестовые данные на границах|
| :---------------------|:----------------------|:-----------------------------|:---------------------------|
| 0  символов           |                       |пустой ввод                   | ~~0 символов - пустой ввод~~ <br/> ~~1 символ - 5~~|
| 1-2 символа           | 1, 2                   |~~2 символа - 35~~                | ~~0 символов - пустой ввод~~ <br/> ~~1 символ - 9~~ <br/> ~~2 символа - 15~~ <br/> ~~3 символа -123~~|
| 3 и более символов    | 3                     |25 символов - 1234567891234567891234567|3 символа -153 <br/> ~~2 символа - 15~~ <br/> 4 символа - 1534|

Обязательность заполнения

| Название класса       | Границы               | Тестовые данные внутри класса| Тестовые данные на границах|
| :---------------------|:----------------------|:-----------------------------|:---------------------------|
| Поле заполнено        |                       |~~15~~                            |                            |
| Поле не заполнено     |                       |~~пустой ввод~~                   |                            |

Негативные проверки

| Название класса       | Тестовые данные внутри класса| 
| :---------------------|:-----------------------------|
| Спец.символы          |@                             |                            
| Буквы                 |два                            |                            
| Дробные числа с запятой|1,5                            |                            
| Дробные числа с точкой |2.2                            |                          
| Дробные числа через /|1/6                           |   
| Отрицательные значения|~~-5~~                           | 

~~Зачёркнутые~~ значения - оптимизация проверок
</details>
<details><summary>Поля ввода адреса (Откуда, Куда)</summary>

*************

Вводимые значения

| Название класса       | Границы               | Тестовые данные внутри класса| Тестовые данные на границах|
| :---------------------|:----------------------|:-----------------------------|:---------------------------|
| Строка с русскими буквами |                  |Ленина                             | |
| Строка с цифрами          |                  |Ленина12                          | |
| Строка с точкой           |                  |Ленина.                        |  |
| Строка с тире           |                  |Ленина-                      |  |
| Строка с запятой           |                  |Ленина,                     |  |
| Строка с пробелом в начале          |                  |" Ленина"                        |  |
| Строка с пробелом в конце          |                  |"Ленина "                        |  |
| Строка с пробелом в середине          |                  |Ленина Ленина                      |  |
| Строка с буквами другого алфавита         |                  |Lenina                      |  |
| Строка с неразрешенными спец.символами          |                  |Ленина@                        |  |
| Строка с дробью         |                  |Ленина1/2                       |  |
| Пустая строка         |                  |пустой ввод                        |  |
| Строка заполненная пробелами          |                  |"   "                        |  |

Длина поля

| Название класса       | Границы               | Тестовые данные внутри класса| Тестовые данные на границах|
| :---------------------|:----------------------|:-----------------------------|:---------------------------|
| от 1 до 50  символов           | 1, 50                     |~~6 символов - Ленина~~                 | 1 символ - Л <br/> 50 символов - ЛенинаЛенинаЛенинаЛенинаЛенинаЛенинаЛенинаЛенинаЛе <br/> ~~0 символов - пустой ввод~~ <br/> 2 символа - Ле <br/> 49 символов - ЛенинаЛенинаЛенинаЛенинаЛенинаЛенинаЛенинаЛенинаЛ <br/> 51 символ - ЛенинаЛенинаЛенинаЛенинаЛенинаЛенинаЛенинаЛенинаЛен|
| 51 символ и более          | 51                   |60 символов - ЛенинаЛенинаЛенинаЛенинаЛенинаЛенинаЛенинаЛенинаЛенинаЛенина|~~51 символ - ЛенинаЛенинаЛенинаЛенинаЛенинаЛенинаЛенинаЛенинаЛен~~ <br/> ~~50 символов - ЛенинаЛенинаЛенинаЛенинаЛенинаЛенинаЛенинаЛенинаЛе~~ <br/> 52 символа - ЛенинаЛенинаЛенинаЛенинаЛенинаЛенинаЛенинаЛенинаЛени|
| 0 символов    |                    |~~0 символов - пустой ввод~~||

Обязательность заполнения

| Название класса       | Границы               | Тестовые данные внутри класса| Тестовые данные на границах|
| :---------------------|:----------------------|:-----------------------------|:---------------------------|
| Поле заполнено        |                       |~~Ленина~~                            |                            |
| Поле не заполнено     |                       |~~пустой ввод~~                   |                            |

~~Зачёркнутые~~ значения - оптимизация проверок
</details>

### Задание 2

**Спроектируй тесты расчёта времени и стоимости**

* Выбери один вид транспорта для тестирования: собственный автомобиль, каршеринг или такси. <br/>
* Определи, какие требования описывают логику расчёта времени и стоимости выбранного транспорта. <br/>
* Напиши формулу, по которой рассчитывается время и стоимость поездки.

* Нарисуй блок-схему, которая визуализирует алгоритм выбора скорости транспорта в зависимости от времени начала поездки.

* Определи классы эквивалентности. И граничные значения каждого класса, к которому это применимо.

* Выбери тестовые значения, которые проверят каждый класс; и границы, если они есть.

* Напиши тест-кейсы на основе тестовых значений. Тест-кейсы должны проверять корректность логики расчёта.

### Решение

> Выбери один вид транспорта для тестирования: собственный автомобиль, каршеринг или такси.

Каршеринг

> Определи, какие требования описывают логику расчёта времени и стоимости выбранного транспорта.

Поля "Начало поездки", "Откуда", "Куда" <br/>
Переключатель режима ("Свой") <br/>
Переключатель вида транспорта ("Каршеринг") <br/>
Средняя скорость автомобиля в зависимости от времени суток <br/>
Стоимость за минуту <br/>
Расстояние между адресами для автомобильных дорог

> Напиши формулу, по которой рассчитывается время и стоимость поездки. 

Время поездки = расстояние / скорость * 60 <br/>
Стоимость поездки = время поездки * стоимость за минуту (9 руб/мин)

> Нарисуй блок-схему, которая визуализирует алгоритм выбора скорости транспорта в зависимости от времени начала поездки.

![SX4cEX1FJH](https://user-images.githubusercontent.com/115216040/208908005-668f5530-b5b8-4f19-814c-e4ec5ec4ff73.png)

[Блок-схема в высоком разрешении](https://miro.com/app/board/uXjVPOvxRY8=/?share_link_id=68226853060)

В соответствии с требованиями, если поездка захватывает несколько временных интервалов, алгоритм выбирает скорость автомобиля из того диапазона, в котором поездка началась.

> Определи классы эквивалентности. И граничные значения каждого класса, к которому это применимо. Выбери тестовые значения, которые проверят каждый класс; и границы, если они есть.

<details><summary>Расстояние между адресами</summary>

| Название класса       | Границы               | Тестовые данные внутри класса| Тестовые данные на границах|
| :---------------------|:----------------------|:-----------------------------|:---------------------------|
| Расстояние > 0 и <br/> AB не = BA |               |Комсомольский проспект, 18 - Зубовский бульвар, 37 <br/> Зубовский бульвар, 37 - Комсомольский проспект, 18                          | |
|Расстояние = 0|                |Зубовский бульвар, 37 - Зубовский бульвар, 37                          | |

</details>

<details><summary>Время начала поездки</summary>

| Название класса       | Границы               | Тестовые данные внутри класса| Тестовые данные на границах|
| :---------------------|:----------------------|:-----------------------------|:---------------------------|
| 00:01 - 08:00 |   [00:01; 08:00]               |04:15                            |00:01 <br/> 08:00 <br/> 00:00 <br/> 00:02 <br/> 07:59 <br/> ~~08:01~~ |
| 08:01 - 12:00         | [08:01; 12:00]                 |10:30                          | 08:01 <br/> 12:00 <br/> ~~08:00~~ <br/> 08:02 <br/> 11:59 <br/> 12:01|
| 12:01-18:00         |  [12:01; 18:00]                |16:45                        |~~12:01~~ <br/> 18:00 <br/> ~~12:00~~ <br/> 12:02 <br/> 17:59 <br/> 18:01 |
| 18:01-22:00          |  [18:01; 22:00]                |20:05                     |~~18:01~~ <br/> ~~22:00~~ <br/> ~~18:00~~ <br/> 18:02 <br/> 21:59 <br/> 22:01  |
| 22:01-00:00          | [22:01; 00:00]             |23:15                     |~~22:01~~ <br/> ~~00:00~~ <br/> 22:00 <br/> 22:02 <br/> 23:59 <br/> ~~00:01~~ |

~~Зачёркнутые~~ значения - оптимизация проверок

</details> 

> Напиши тест-кейсы на основе тестовых значений. Тест-кейсы должны проверять корректность логики расчёта.

Расчёт времени и стоимости поездки на автомобиле, взятом в каршеринг:
   
   <dl>
  <dt>Входные данные:</dt>
  <dd>Время начала поездки (5 тестовых значений). Взяты значения только внутри диапозонов. <br/>
   Расстояние между адресами (3 тестовых значения). Расстояние = 0, расстояние > 0, расстояние AB не = BA. <br/>
   Точка А (Откуда): Комсомольский проспект, 18 <br/>
   Точка Б (Куда): Зубовский бульвар, 37 <br/> </dd>

  <dt>Расчёт:</dt>
  <dd>Время поездки, формула: расстояние (2,9 км) / средняя скорость автомобиля * 60 <br/>
   Стоимость поездки, формула: время поездки * стоимость за 1 минуту (9 руб.)</dd>
   
   <dt>Выходные данные: </dt>
  <dd>Время в пути <br/>
   Стоимость поездки</dd>
</dl>

   
<details><summary>Тест-кейсы</summary>

| id тест-кейса | Название тест-кейса| Предусловия | Описание шагов | ОР                        | 
|:------------- |:------------------|:-------------|:-----------------|:-------------------------|
| t-1| Время движения и стоимость поездки автомобиля, взятого в каршеринг, в Яндекс.Маршрутах при времени начала движения - 18:01-22:00 |Открыть сервис Яндекс.Маршруты| 1. Ввести время начала поездки - 20:05 <br/> 2. Ввести в поле "Откуда" Комсомольский проспект, 18 <br/> 3. Ввести в поле "Куда" Зубовский бульвар, 37 <br/> 4. Выбрать маршрут "Свой" <br/> 5. Выбрать вид транспорта "Каршеринг" |На экране отображается: <br/> Время движения - 7 минут; <br/> Стоимость поездки - 63 руб.
|t-2     |Время движения и стоимость поездки автомобиля, взятого в каршеринг, в Яндекс.Маршрутах при времени начала движения - 22:01 - 00:00 | Открыть сервис Яндекс.Маршруты |1. Ввести время начала поездки - 23:15 <br/> 2. Ввести в поле "Откуда" Комсомольский проспект, 18 <br/> 3. Ввести в поле "Куда" Зубовский бульвар, 37 <br/> 4. Выбрать маршрут "Свой" <br/> 5. Выбрать вид транспорта "Каршеринг"|На экране отображается: <br/> Время движения - 4 минуты; <br/> Стоимость поездки - 36 руб.|
| t-3| Время движения и стоимость поездки автомобиля, взятого в каршеринг, в Яндекс.Маршрутах при времени начала движения - 00:01 - 08:00 |Открыть сервис Яндекс.Маршруты| 1. Ввести время начала поездки - 04:15 <br/> 2. Ввести в поле "Откуда" Комсомольский проспект, 18 <br/> 3. Ввести в поле "Куда" Зубовский бульвар, 37 <br/> 4. Выбрать маршрут "Свой" <br/> 5. Выбрать вид транспорта "Каршеринг" |На экране отображается: <br/> Время движения - 4 минуты; <br/> Стоимость поездки - 36 руб.|
| t-4| Время движения и стоимость поездки автомобиля, взятого в каршеринг, в Яндекс.Маршрутах при времени начала движения - 08:01 - 12:00 |Открыть сервис Яндекс.Маршруты| 1. Ввести время начала поездки - 10:30 <br/> 2. Ввести в поле "Откуда" Комсомольский проспект, 18 <br/> 3. Ввести в поле "Куда" Зубовский бульвар, 37 <br/> 4. Выбрать маршрут "Свой" <br/> 5. Выбрать вид транспорта "Каршеринг" |На экране отображается: <br/> Время движения - 6 минут; <br/> Стоимость поездки - 54 руб.|
| t-5| Время движения и стоимость поездки автомобиля, взятого в каршеринг, в Яндекс.Маршрутах при времени начала движения - 12:01 - 18:00 |Открыть сервис Яндекс.Маршруты| 1. Ввести время начала поездки - 20:05 <br/> 2. Ввести в поле "Откуда" Комсомольский проспект, 18 <br/> 3. Ввести в поле "Куда" Зубовский бульвар, 37 <br/> 4. Выбрать маршрут "Свой" <br/> 5. Выбрать вид транспорта "Каршеринг" |На экране отображается: <br/> Время движения - 5 минут; <br/> Стоимость поездки - 45 руб.|
| t-6| Время движения и стоимость поездки автомобиля, взятого в каршеринг, в Яндекс.Маршрутах при указании в полях "Откуда" и "Куда" одного и того же адреса |Открыть сервис Яндекс.Маршруты| 1. Ввести время начала поездки - 20:05 <br/> 2. Ввести в поле "Откуда" Зубовский бульвар, 37 <br/> 3. Ввести в поле "Куда" Зубовский бульвар, 37 <br/> 4. Выбрать маршрут "Свой" <br/> 5. Выбрать вид транспорта "Каршеринг" |На экране отображается: <br/> Время движения - 0 минут; <br/> Стоимость поездки - 0 руб.|
| t-7| Время движения и стоимость поездки автомобиля, взятого в каршеринг, в Яндекс.Маршрутах при перемене местами значений в полях "Откуда" и "Куда", в случаях, когда расстояние туда и обратно не совпадают |Открыть сервис Яндекс.Маршруты| 1. Ввести время начала поездки - 20:05 <br/> 2. Ввести в поле "Откуда" Зубовский бульвар, 37 <br/> 3. Ввести в поле "Куда" Комсомольский проспект, 18 <br/> 4. Выбрать маршрут "Свой" <br/> 5. Выбрать вид транспорта "Каршеринг" |На экране отображается: <br/> Время движения - 4 минуты; <br/> Стоимость поездки - 36 руб.|
</details>

## Тестирование веб-приложений

<details><summary>Задание</summary>


**1. Проанализируй [макеты](https://www.figma.com/file/42mNwme0cBfZwNZUIcN1mh/%D0%AF%D0%BD%D0%B4%D0%B5%D0%BA%D1%81.%D0%9C%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82%D1%8B?node-id=2%3A18586) и [требования](https://praktikum.notion.site/07f02ccc272e494db6501def032e9258) к каршерингу.**

Если требования и макеты не сходятся — ориентируйся на требования.

**2. Подготовь тестовую документацию, чтобы проверить вёрстку формы бронирования и навигационной карты.**

Внимательно изучи макеты каршеринга в Figma — вкладка «Marshruti car sharing».
        
Составь чек-лист, по которому будешь тестировать вёрстку формы бронирования и навигационной карты.

Выбери только один тариф. Например, «Роскошный».

Валидацию полей, а также вёрстку окон «Добавление прав», «Способ оплаты», «Добавление карты» тестировать не нужно.

**3. Подготовь тестовую документацию, чтобы проверить логику работы.**

Проанализируй требования к функциональности каршеринга.
        
Составь чек-лист, по которому будешь проверять функциональность окон «Способ оплаты» и «Добавление карты». 

Подготовь тест-кейсы:
        
* На логику работы кнопки «Забронировать» — см. пункт требований «Кнопка “Забронировать”».
        
* На логику функциональности бронирования — см. пункт требований «Бронь машины»
        
> Обрати внимание:

* На кнопке «Забронировать» указаны расстояние и время в пути. Например: «Маршрут составит 3 км и займёт 4 мин». Тебе не нужно проверять, правильно ли рассчитаны эти данные.
* Таймер, который отсчитывает время бесплатного ожидания, тестировать также не нужно.

**4. Протестируй приложение и заведи баг-репорты**

Протестируй функциональность каршеринга по чек-листам и тест-кейсам, которые тебе удалось спроектировать ранее. Времени на проверку осталось мало, поэтому используй только две конфигурации окружения:
        
* Яндекс.Браузер при разрешении экрана 800x600;
* Firefox при разрешении экрана 1920x1080.
        
Тестирование вёрстки нужно провести в обоих окружениях. Логику приложения достаточно проверить в одном окружении.

Когда будешь тестировать, отмечай результаты выполнения проверок: PASSED, FAILED или SKIPPED (англ. «пропущен»). 
        
Если тест со статусом FAILED —заведи баг-репорты в YouTrack. Не забудь вписать ID в соответствующую таблицу результатов.
> Обрати внимание:

В требованиях сказано, что после заполнения поля «Добавить права» включается таймер на 30 секунд. В текущей реализации его нет. Разработчики специально передали тестовый стенд: так тебе не придётся ждать каждый раз, когда выполняешь проверку.

**5. Подведение итогов**

Представь, что тебе нужно рассказать команде о статусе протестированной части продукта:

* Какое впечатление оставил у тебя сервис как у пользователя?
* Расскажи, что именно тебе удалось протестировать в нескольких предложениях.
* Подведи итоги тестирования: например, тебе удалось провести все тесты и найти несколько багов. Приложи ссылки на них, чтобы коллеги могли их быстро открыть и посмотреть.
* Сделай вывод: как ты думаешь, можно ли отдать такой продукт пользователям, или его нужно доработать. Помни, тестировщик даёт рекомендации, а итоговое решение принимает команда менеджеров.
</details>

### Решение

**1. Тестовая документация для вёрстки**
<details><summary>Чек-лист</summary>

| №     | Описание проверки              | Статус <br/> Яндекс.Браузер, 800x600|Статус <br/> Firefox, 1920x1080|Ссылка на баг-репорт|
|:-----:|:----------------------|:-----------------------------|:---------------------------|:-------------:|
| 1| Стартовое состояние формы бронирования - выбран тариф Повседневный, поля «Добавить права» и «Способ оплаты» пустые|:white_check_mark:PASSED|:white_check_mark:PASSED |
| 2| Для выбора доступно три тарифа: Повседневный, Походный, Роскошный|:white_check_mark:PASSED| :white_check_mark:PASSED|
| 3| Элемент тарифа состоит из иконки автомобиля, названия тарифа, цены|:white_check_mark:PASSED| :white_check_mark:PASSED|
| 4| Выбранный тариф подсвечивается серым|:white_check_mark:PASSED| :white_check_mark:PASSED|
| 5| Надписи выбранного элемента меняется с серого на черный|:white_check_mark:PASSED| :white_check_mark:PASSED|
| 6| Надписи не выходят за границы элемента|:white_check_mark:PASSED| :white_check_mark:PASSED|
| 7| В элементах тарифов нет орфографических ошибок |:white_check_mark:PASSED| :white_check_mark:PASSED|
| 8|В левом верхнем углу формы бронирования располагается белая стрелка в сером кружке для перехода обратно к выбору режима |:x:FAILED| :x:FAILED| [BUG-1](https://vladazakharova.youtrack.cloud/issue/S2-11)
| 9| Под панелью выбора тарифов расположен блок с деталями тарифа и информацией о ближайшей машине|:white_check_mark:PASSED| :white_check_mark:PASSED|
| 10| Вверху блока с деталями, по середине, расположен заголовок - название марки машины - BMW 750, цвет черный, шрифт жирный |:white_check_mark:PASSED|:white_check_mark:PASSED|
| 11| Под названием марки машины, по середине, расположено описание тарифа "Просто по делам, ничего лишнего", цвет надписи черный|:white_check_mark:PASSED|:white_check_mark:PASSED|
| 12|Под описанием тарифа, по середине, расположена информация о времени в пути от пункта «Откуда» до машины и времени бесплатного ожидания, "4 мин • 15 мин бесплатного ожидания", цвет текста серый, шрифт меньше чем у описания тарифа|:x:FAILED| :x:FAILED| [BUG-2](https://vladazakharova.youtrack.cloud/issue/S2-2)|
| 13|Рядом с временем в пути до машины, слева, находится серая картинка человечка, размер картинки равен размеру текста |:x:FAILED| :x:FAILED| [BUG-3](https://vladazakharova.youtrack.cloud/issue/S2-3)|       
| 14|Информация о времени в пути и о времени бесплатного ожидания разделена жирной серой точкой между ними |:x:FAILED| :x:FAILED| [BUG-4](https://vladazakharova.youtrack.cloud/issue/S2-4 )|
| 15| Под информацией о времени в пути и временем бесплатного ожидания, по середине, располагается изображение машины серого цвета, изображении не менее 1/3 блока с информацией о тарифе|:white_check_mark:PASSED| :white_check_mark:PASSED|
| 16| Под изображением машины, по середине, расположена информация о доп. параметрах, цвет текста серый, шрифт такой же как у информации о времени в пути до машины и времени бесплатного ожидания|:white_check_mark:PASSED| :white_check_mark:PASSED|
| 17| Для тарифа Повседневный в доп. параметрах отображаются "видеорегистратор • зарядка для телефона"|:white_check_mark:PASSED| :white_check_mark:PASSED|
| 18|Доп. параметры расположены в одну строчку и разделены серой жирной точкой |:x:FAILED| :x:FAILED| [BUG-5](https://vladazakharova.youtrack.cloud/issue/S2-5)|
| 19|Текстовая информация не выходит за границы блока с деталями тарифа  |:white_check_mark:PASSED| :white_check_mark:PASSED|
| 20|В блоке нет орфографических ошибок |:white_check_mark:PASSED| :white_check_mark:PASSED| 
| 21|Информация о времени в пути и о времени бесплатного ожидания разделена жирной серой точкой между ними |:white_check_mark:PASSED| :x:FAILED| [BUG-6](https://vladazakharova.youtrack.cloud/issue/S2-6)|
| 22|На карте автоматически выбрана машина, которая находится ближе всего к пользователю, иконка ближайшей машины увеличивается|:x:FAILED| :x:FAILED| [BUG-7](https://vladazakharova.youtrack.cloud/issue/S2-7)|
| 23|Над иконкой ближайшей машины появляется чёрная плашка с маркой машины|:x:FAILED| :x:FAILED| [BUG-8](https://vladazakharova.youtrack.cloud/issue/S2-9)|
| 24| Остальные свободные машины продолжают отображаться на карте в виде иконок автомобилей|:white_check_mark:PASSED| :white_check_mark:PASSED|
| 25| На карте отображаются автомобили всех тарифов|:white_check_mark:PASSED| :white_check_mark:PASSED|
| 26|Пользователь может выбрать машину на карте, при нажатии на иконку, она увеличивается, над ней появляется чёрная плашка с маркой, а на левой панели — обновлённая информация о машине|:x:FAILED| :x:FAILED| [BUG-9](https://vladazakharova.youtrack.cloud/issue/S2-8)|
| 27|Иконки машин направлены в разные стороны|:x:FAILED| :x:FAILED| [BUG-10](https://vladazakharova.youtrack.cloud/issue/S2-10)|
| 28| Иконки машин расположены обособленно относительно других элементов на карте, расположены на дорогах |:white_check_mark:PASSED| :white_check_mark:PASSED|
| 29| На карте маршрут отображен фиолетовой линией от красной точкой А до синей точки В|:white_check_mark:PASSED| :white_check_mark:PASSED|
| 30| Под блоком с деталями тарифа расположено поле «Добавить права», цвет текста Добавить права - серый |:white_check_mark:PASSED| :white_check_mark:PASSED|
| 31| Текст поля не выходит за его границы |:white_check_mark:PASSED| :white_check_mark:PASSED|
| 32|В правом углу поля Добавить права размещена кнопка ">" |:x:FAILED| :x:FAILED| [BUG-11](https://vladazakharova.youtrack.cloud/issue/S2-12)|
| 33|Если документы прошли верификацию, рамка поля подсвечивается зелёным, у правого края внутри поля появляется зелёная галочка |:x:FAILED| :x:FAILED| [BUG-12](https://vladazakharova.youtrack.cloud/issue/S2-13 )|
| 34|Если документы не прошли верификацию, рамка поля подсвечивается красным, у правого края внутри поля появляется красный крестик |:fast_forward:SKIPPED| :fast_forward:SKIPPED| [BUG-13](https://vladazakharova.youtrack.cloud/issue/S2-14)|
| 35| Под полем Добавить права расположено поле "Способ оплаты", текст "Способ оплаты" черного цвета |:white_check_mark:PASSED| :white_check_mark:PASSED|
| 36| В правой половине поля "Способ оплаты" расположен серый текст "Добавить", иконка банковской карты и черная стрелка, направленная вправо ">"|:white_check_mark:PASSED| :white_check_mark:PASSED|
| 37| Текст не выходит за границы поля |:white_check_mark:PASSED| :white_check_mark:PASSED|
| 38| В надписях кнопки нет орфографических ошибок|:white_check_mark:PASSED| :white_check_mark:PASSED|
| 39| Если карта уже добавлена текст меняется с "Добавить" на "Карта", цвет текста серый|:white_check_mark:PASSED| :white_check_mark:PASSED|

</details>
