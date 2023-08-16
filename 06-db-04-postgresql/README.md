# Домашнее задание к занятию 4. «PostgreSQL»

## Задача 1

Используя Docker, поднимите инстанс PostgreSQL (версию 13). Данные БД сохраните в volume.

![1](https://github.com/AlexanderM33/bd-dev-homeworks/assets/122460278/b609734d-30fb-4657-80fd-0723bff92144)

```
docker pull postgres:13
docker volume create homework
docker image tag postgres:13 mishindb
docker run --rm --name mishindb -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres -ti -p 5432:5432 -v homework:/var/lib/postgresql/data postgres:13
docker exec -ti mishindb bash
```

Подключитесь к БД PostgreSQL, используя `psql`.

Воспользуйтесь командой `\?` для вывода подсказки по имеющимся в `psql` управляющим командам.

**Найдите и приведите** управляющие команды для:

- вывода списка БД,  `\l[+] [PATTERN] list databases`
- подключения к БД, `\c[onnect] {[DBNAME|- USER|- HOST|- PORT|-] | conninfo}
 connect to new database (currently "postgres")`
- вывода списка таблиц, `\d[S+] или \dt[S+]`
- вывода описания содержимого таблиц, `\dS+ или \dtS+`
- выхода из psql. `\q`

Несколько скринов
![3](https://github.com/AlexanderM33/bd-dev-homeworks/assets/122460278/62175b3e-6d70-48f5-9bed-612f54125b68)

![2](https://github.com/AlexanderM33/bd-dev-homeworks/assets/122460278/9b3027a4-3692-4896-94c8-f1381190b1cc)




## Задача 2

Используя `psql`, создайте БД `test_database`.

Изучите [бэкап БД](https://github.com/netology-code/virt-homeworks/tree/virt-11/06-db-04-postgresql/test_data).

Восстановите бэкап БД в `test_database`.

Перейдите в управляющую консоль `psql` внутри контейнера.

Подключитесь к восстановленной БД и проведите операцию ANALYZE для сбора статистики по таблице.

Используя таблицу [pg_stats](https://postgrespro.ru/docs/postgresql/12/view-pg-stats), найдите столбец таблицы `orders` 
с наибольшим средним значением размера элементов в байтах.

**Приведите в ответе** команду, которую вы использовали для вычисления, и полученный результат.

![4](https://github.com/AlexanderM33/bd-dev-homeworks/assets/122460278/97150fe0-1a3f-4b89-863d-b314d7dadb52)

`16`


## Задача 3

Архитектор и администратор БД выяснили, что ваша таблица orders разрослась до невиданных размеров и
поиск по ней занимает долгое время. Вам как успешному выпускнику курсов DevOps в Нетологии предложили
провести разбиение таблицы на 2: шардировать на orders_1 - price>499 и orders_2 - price<=499.

Предложите SQL-транзакцию для проведения этой операции.


![5](https://github.com/AlexanderM33/bd-dev-homeworks/assets/122460278/bdbdc890-cde6-4ea9-a469-8365231b2c2a)

Можно ли было изначально исключить ручное разбиение при проектировании таблицы orders?

`Можно, если задумать разделение на этапе проектирования сиспользованием шардирования`

## Задача 4

Используя утилиту `pg_dump`, создайте бекап БД `test_database`.

![6](https://github.com/AlexanderM33/bd-dev-homeworks/assets/122460278/10d39c08-f159-4ac0-bf7b-0127123cecfe)


Как бы вы доработали бэкап-файл, чтобы добавить уникальность значения столбца `title` для таблиц `test_database`?

`Для этого можно добавить индекс`

---

### Как cдавать задание

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---

