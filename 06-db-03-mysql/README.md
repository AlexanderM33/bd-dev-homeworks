# Домашнее задание к занятию 3. «MySQL»



## Задача 1

Используя Docker, поднимите инстанс MySQL (версию 8). Данные БД сохраните в volume.

Изучите [бэкап БД](https://github.com/netology-code/virt-homeworks/tree/virt-11/06-db-03-mysql/test_data) и 
восстановитесь из него.

![1](https://github.com/AlexanderM33/bd-dev-homeworks/assets/122460278/ea561b79-5143-41cd-883a-cb80093c2950)


Перейдите в управляющую консоль `mysql` внутри контейнера.

Используя команду `\h`, получите список управляющих команд.

![2](https://github.com/AlexanderM33/bd-dev-homeworks/assets/122460278/8b19ce28-db2a-4057-8a80-c28ba8ce5101)


Найдите команду для выдачи статуса БД и **приведите в ответе** из её вывода версию сервера БД.

![3](https://github.com/AlexanderM33/bd-dev-homeworks/assets/122460278/a50d4215-2bc9-45c2-9a5d-3292db1beff2)

Подключитесь к восстановленной БД и получите список таблиц из этой БД.

![4](https://github.com/AlexanderM33/bd-dev-homeworks/assets/122460278/7c03451b-f8b0-49e3-9234-1fa03a9076de)

**Приведите в ответе** количество записей с `price` > 300.



В следующих заданиях мы будем продолжать работу с этим контейнером.

## Задача 2

Создайте пользователя test в БД c паролем test-pass, используя:

- плагин авторизации mysql_native_password
- срок истечения пароля — 180 дней 
- количество попыток авторизации — 3 
- максимальное количество запросов в час — 100
- аттрибуты пользователя:
    - Фамилия "Pretty"
    - Имя "James".

![5](https://github.com/AlexanderM33/bd-dev-homeworks/assets/122460278/a074f241-5889-4d37-a955-809ce9bc4ac8)

Предоставьте привелегии пользователю `test` на операции SELECT базы `test_db`.
    
Используя таблицу INFORMATION_SCHEMA.USER_ATTRIBUTES, получите данные по пользователю `test` и 
**приведите в ответе к задаче**.



## Задача 3

Установите профилирование `SET profiling = 1`.
Изучите вывод профилирования команд `SHOW PROFILES;`.

Исследуйте, какой `engine` используется в таблице БД `test_db` и **приведите в ответе**.

Измените `engine` и **приведите время выполнения и запрос на изменения из профайлера в ответе**:
- на `MyISAM`,
- на `InnoDB`.
![7](https://github.com/AlexanderM33/bd-dev-homeworks/assets/122460278/7d0534c8-5090-44c6-a49a-b4ad6b10da6f)


![8](https://github.com/AlexanderM33/bd-dev-homeworks/assets/122460278/39d45687-0820-4c4c-b524-a43e5b7031d7)



## Задача 4 

Изучите файл `my.cnf` в директории /etc/mysql.

Измените его согласно ТЗ (движок InnoDB):

- скорость IO важнее сохранности данных;
- нужна компрессия таблиц для экономии места на диске;
- размер буффера с незакомиченными транзакциями 1 Мб;
- буффер кеширования 30% от ОЗУ;
- размер файла логов операций 100 Мб.

Приведите в ответе изменённый файл `my.cnf`.

![9](https://github.com/AlexanderM33/bd-dev-homeworks/assets/122460278/a370ce91-e9fa-422d-a734-648c45513348)


```
[mysqld]

skip-host-cache
skip-name-resolve
datadir=/var/lib/mysql
socket=/var/run/mysqld/mysqld.sock
secure-file-priv=/var/lib/mysql-files
user=mysql

pid-file=/var/run/mysqld/mysqld.pid
[client]
socket=/var/run/mysqld/mysqld.sock

!includedir /etc/mysql/conf.d/
innodb_flush_log_at_trx_commit = 0
innodb_file_per_table = ON
innodb_log_buffer_size = 1M
innodb_buffer_pool_size = 4G
innodb_log_file_size = 100M

```

---

### Как оформить ДЗ

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---

