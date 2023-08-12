# Домашнее задание к занятию 2. «SQL»

## Введение

Перед выполнением задания вы можете ознакомиться с 
[дополнительными материалами](https://github.com/netology-code/virt-homeworks/blob/virt-11/additional/README.md).

## Задача 1

Используя Docker, поднимите инстанс PostgreSQL (версию 12) c 2 volume, 
в который будут складываться данные БД и бэкапы.

Приведите получившуюся команду или docker-compose-манифест.

```
docker run --name postgres_mishin -p 5432:5432 -e POSTGRES_USER=test-admin-user -e POSTGRES_PASSWORD=qweqwe -v '/var/lib/postgresql/data' -v '/tmp/backup' postgres:12
```

## Задача 2

В БД из задачи 1: 

- создайте пользователя test-admin-user и БД test_db;
- в БД test_db создайте таблицу orders и clients (спeцификация таблиц ниже);
- предоставьте привилегии на все операции пользователю test-admin-user на таблицы БД test_db;
- создайте пользователя test-simple-user;
- предоставьте пользователю test-simple-user права на SELECT/INSERT/UPDATE/DELETE этих таблиц БД test_db.

Таблица orders:

- id (serial primary key);
- наименование (string);
- цена (integer).

Таблица clients:

- id (serial primary key);
- фамилия (string);
- страна проживания (string, index);
- заказ (foreign key orders).

Приведите:

- итоговый список БД после выполнения пунктов выше;
- описание таблиц (describe);
- SQL-запрос для выдачи списка пользователей с правами над таблицами test_db;
- список пользователей с правами над таблицами test_db.

![2](https://github.com/AlexanderM33/bd-dev-homeworks/assets/122460278/5df76eba-5cde-4cce-a611-22a9a94eb725)

![1](https://github.com/AlexanderM33/bd-dev-homeworks/assets/122460278/f77ec1f6-b179-418c-8474-79f6085c7936)

![3](https://github.com/AlexanderM33/bd-dev-homeworks/assets/122460278/c9103975-7908-4343-a853-6164a31a1e56)



## Задача 3

Используя SQL-синтаксис, наполните таблицы следующими тестовыми данными:

Таблица orders

|Наименование|цена|
|------------|----|
|Шоколад| 10 |
|Принтер| 3000 |
|Книга| 500 |
|Монитор| 7000|
|Гитара| 4000|

Таблица clients

|ФИО|Страна проживания|
|------------|----|
|Иванов Иван Иванович| USA |
|Петров Петр Петрович| Canada |
|Иоганн Себастьян Бах| Japan |
|Ронни Джеймс Дио| Russia|
|Ritchie Blackmore| Russia|

Используя SQL-синтаксис:
- вычислите количество записей для каждой таблицы.

Приведите в ответе:

    - запросы,
    - результаты их выполнения.

![5](https://github.com/AlexanderM33/bd-dev-homeworks/assets/122460278/85d71913-8752-4711-860a-be5d02944dc1)


## Задача 4

Часть пользователей из таблицы clients решили оформить заказы из таблицы orders.

Используя foreign keys, свяжите записи из таблиц, согласно таблице:

|ФИО|Заказ|
|------------|----|
|Иванов Иван Иванович| Книга |
|Петров Петр Петрович| Монитор |
|Иоганн Себастьян Бах| Гитара |

Приведите SQL-запросы для выполнения этих операций.

Приведите SQL-запрос для выдачи всех пользователей, которые совершили заказ, а также вывод этого запроса.
 
Подсказка: используйте директиву `UPDATE`.

![6](https://github.com/AlexanderM33/bd-dev-homeworks/assets/122460278/5e16d2ac-8324-4517-936e-3c642c034b12)


## Задача 5

Получите полную информацию по выполнению запроса выдачи всех пользователей из задачи 4 
(используя директиву EXPLAIN).

Приведите получившийся результат и объясните, что значат полученные значения.

![7](https://github.com/AlexanderM33/bd-dev-homeworks/assets/122460278/99133c47-ae86-4adb-8bda-b73120a72e05)

Используется метод последовательного чтения данных метода Seq Scan. Значение 0.00 —  это ожидаемые затраты на получение первой строки. Второе — 22.00 — ожидаемые затраты на получение всех строк. rows - ожидаемое число строк 1200, которое должен вывести этот узел. Width 32 - ожидаемый средний размер строк, выводимых этим узлом плана (в байтах). Materealize -это реальное выполнение запроса




## Задача 6

Создайте бэкап БД test_db и поместите его в volume, предназначенный для бэкапов (см. задачу 1).
```
docker exec 9d10c7e4be57 pg_dump -U test-admin-user -d test_db -Fc -f /var/lib/postgresql/backups/backup_file.dump
```

Остановите контейнер с PostgreSQL, но не удаляйте volumes.
```
docker stop 9d10c7e4be57
```

Поднимите новый пустой контейнер с PostgreSQL.
```
docker run --name postgres_mishin777 -p 5432:5432 -e POSTGRES_USER=test-admin-user -e POSTGRES_PASSWORD=qweqwe -v '/var/lib/postgresql/data' -v '/tmp/backup' postgres:12
```

Восстановите БД test_db в новом контейнере.
```
docker exec -it postgres_mishin7 pg_restore -U test-admin-user -Ft -v -d test_db /var/lib/postgresql/backups/backup_file.dump
```
Приведите список операций, который вы применяли для бэкапа данных и восстановления. 

---

### Как cдавать задание

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---

