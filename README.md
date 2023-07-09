# Домашнее задание к занятию «Базы данных»

---
### Легенда

Заказчик передал вам [файл в формате Excel](https://github.com/netology-code/sdb-homeworks/blob/main/resources/hw-12-1.xlsx), в котором сформирован отчёт. 

На основе этого отчёта нужно выполнить следующие задания.

### Задание 1

Опишите не менее семи таблиц, из которых состоит база данных:

- какие данные хранятся в этих таблицах;
- какой тип данных у столбцов в этих таблицах, если данные хранятся в PostgreSQL.

Приведите решение к следующему виду:

Сотрудники (

- идентификатор, первичный ключ, serial,
- фамилия varchar(50),
- ...
- идентификатор структурного подразделения, внешний ключ, integer).

Ответ:

- какие данные хранятся в этих таблицах
1. ФИО сотрудника – фамилия, имя и отчество сотрудников
2. Оклад – заработная плата сотрудников
3. Должность – занимаемая должность сотрудников
4. Тип подразделения – отдел, в котором работают сотрудники
5. Структурное подразделение – наименование филиала, в котором работают сотрудники
6. Дата найма – дата приема на работу сотрудников
7. Адрес филиала – местонахождение филиала (край\область, город, улица, дом)
8. Проект на который назначен – наименование проекта, с которым работает конкретный сотрудник
- какой тип данных у столбцов в этих таблицах, если данные хранятся в PostgreSQL.
1. ФИО сотрудника –VARCHAR – строка переменной длины
2. Оклад – DECIMAL/NUMERIC – число с плавающей точкой
3. Должность – VARCHAR – строка переменной длины
4. Тип подразделения – VARCHAR – строка переменной длины
5. Структурное подразделение – VARCHAR – строка переменной длины
6. Дата найма – MEDIUMINT — целое число среднего размера. Хотел поставить DATE – дата, но формат вывода не подходит.
7. Адрес филиала – VARCHAR – строка переменной длины
8. Проект на который назначен – VARCHAR – строка переменной длины

Привожу решение к следующему виду:
Оставляю не тронутыми: оклад, проект на который назначен



Таблица №1	Основная

```
employees (
employee_id primary_key, 
first_name varchar(50),
last_name varchar(50),
patronymic varchar(50),			отчество
salary_id numeric,				оклад
position_id varchar(50),			должность
type_of_division_id varchar(50),		тип подразделения
structural_division_id varchar(50),		структурное подразделение
date_of_hiring mediumint(50),		дата найма
branch_address_id varchar(50), 		адрес филиала
project_id varchar(50),			проект, на который назначен
)
```

Таблица №2

```
salary (
salary_id primary_key,
salary_name numeric,
)
```

Таблица №3

```
position (
position_id primary_key,
position_name varchar(50),
)
```

Таблица №4

```
type_of_division (
type_of_division_id primary_key,
type_of_division_name varchar(50),
)
```

Таблица №5

```
structural_division (
structural_division_id primary_key,
structural_division_name varchar(50),
)
```

Таблица №6

```
branch_address (
branch_address_id primary_key,
branch_address_name varchar(50),
)
```

Таблица №7

```
project (
project primary_key,
project_name varchar(50),
)
```

Еще есть идея разбить таблицу адреса филиала на 4 и соединить с основной таблицей с помощью внешнего ключа

Получаю

Таблица №8

```
branch_address (
branch_address_id primary_key,
edge_or_region varchar(50),
city_id varchar(50),
street_id varchar(50),
house_id numeric,
)
```

Таблица №9

```
edge_or_region (
edge_or_region_id primary_key,
edge_or_region_name varchar(50),
)
```

Таблица №10

```
city (
city_id primary_key,
city_name,
)
```

Таблица №11

```
street (
street_id primary_key,
street_name varchar(50),
)
```

Таблица №12

```
house (
house_id primary_key,
house_name numeric,
)
```


## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.


### Задание 2*

Перечислите, какие, на ваш взгляд, в этой денормализованной таблице встречаются функциональные зависимости и какие правила вывода нужно применить, чтобы нормализовать данные.
