# Тестовое задание для отбора на Летнюю ИТ-школу КРОК по разработке

## Условие задания
Один развивающийся и перспективный маркетплейс активно растет в настоящее время. Текущая команда разработки вовсю занята тем, что развивает ядро системы. Помимо этого, перед CTO маркетплейса стоит задача — разработать подсистему аналитики, которая на основе накопленных данных формировала бы разнообразные отчеты и статистику.

Вы — компания подрядчик, с которой маркетплейс заключил рамочный договор на выполнение работ по разработке этой подсистемы. В рамках первого этапа вы условились провести работы по прототипированию и определению целевого технологического стека и общих подходов к разработке.

На одном из совещаний с Заказчиком вы определили задачу, на которой будете выполнять работы по прототипированию. В качестве такой задачи была выбрана разработка отчета о периодах наибольших трат со стороны пользователей.

Аналитики со стороны маркетплейса предоставили небольшой срез массива данных (файл format.json) о покупках пользователей, на примере которого вы смогли бы ознакомиться с форматом входных данных. Каждая запись данного среза содержит следующую информацию:
- Идентификатор пользователя;
- Дата и время оформления заказа;
- Статус заказа;
- Сумма заказа.

В пояснительной записке к массиву данных была уточняющая информация относительно статусов заказов:
- COMPLETED (Завершенный заказ);
- CANCELED (Отмененный заказ);
- CREATED (Созданный заказ, еще не оплаченный);
- DELIVERY (Созданный и оплаченный заказ, который доставляется).

Необходимо разработать отчет, вычисляющий по полученному массиву данных месяц, когда пользователи тратили больше всего. Если максимальная сумма пользовательских трат была в более, чем одном месяце, отчет должен показывать все такие месяцы. В отчете должны учитываться только завершенные заказы.

Требования к реализации:
1. Реализация должна содержать, как минимум, одну процедуру (функцию/метод), отвечающую за формирование отчета, и должна быть описана в readme.md в соответствии с чек-листом;
2. В качестве входных данных программа использует json-файл (input.json), соответствующий структуре, описанной в условиях задания;
3. Процедура (функция/метод) формирования отчета должна возвращать строку в формате json следующего формата:
   - {«months»: [«march»]} 
   - {«months»: [«march», «december»]}
4. Найденный в соответствии с условием задачи месяц должен выводиться на английском языке в нижнем регистре. Если месяцев несколько, то на вывод они все подаются на английском языке в нижнем регистре в порядке их следования в течение года.

## Автор решения
Заволокин Иван
## Описание реализации
Извлекаются данные из JSON-файла о затратах за заказы, определяются месяцы с наибольшими суммарными затратами и создается отчет в формате JSON. Весь процесс организован с помощью двух функций.

Функция, `report_generation`, открывает файл JSON и загружает его содержимое в словарь `format_dict`. Затем создается пустой словарь `month`, в котором будет храниться информация о суммарных затратах по месяцам. Цикл проходит по данным из `format_dict`, проверяя статус заказа (завершен ли он), в словарь  `month` добавляются пары ключ значения, где ключ - это месяц в числовом формате, а значение - затраты в месяце. Если ключ уже есть в словаре, то затраты добавляются к значению. После обработки всех данных функция вызывает `find_max_month` для определения месяцев с максимальными затратами, создает словарь с этой информацией и преобразует его в формат JSON. В итоге функция возвращает JSON-строку, содержащую информацию о месяцах с наибольшими затратами.

Функция, `find_max_month`, ищет месяцы с наибольшей суммой затрат. В начале создается список `month_list`, который будет содержать месяцы с максимальными затратами. Затем функция сортирует словарь `month` в порядке убывания значений, чтобы первым оказался месяц с наибольшей суммой затрат. Далее происходит проход по отсортированному словарю, и если значение текущего месяца больше или равно `max_value`, оно добавляется в список `month_list`, затем `max_value` обновляется. Процесс продолжается до тех пор, пока не будет достигнут месяц с меньшим значением затрат. Затем функция сортирует месяцы в порядке их следования и преобразует числовые обозначения месяцев в их текстовые названия в нижнем регистре.



## Инструкция по сборке и запуску решения
Установить необходимый системный компонент:
   - python 3.11.
   
Разместить файл с данными в формате json в той же дирректории, что и исполняемый файл main.py.
Для запука выполнить команду `python main.py` для windows. Или для linux `main.py`.
