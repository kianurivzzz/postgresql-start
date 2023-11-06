# Инструкция по установке PostgreSQL и DBeaver.

## Для Windows
Установка всех программ происходит через графические интерфейсы и сайты, поэтому всё просто, но долго.
### Установка PostgreSQL
1. Перейдите на [официальный сайт PostgreSQL](https://www.postgresql.org/download/windows/).
2. Прокрутите страницу вниз до раздела "Interactive installer by BigSQL" или "Graphical Installer by EDB". Выберите ссылку для загрузки соответствующего инсталлятора.
3. Запустите загруженный инсталлятор и следуйте инструкциям установщика.
4. Во время установки вам будет предложено указать пароль для пользователя postgres. Запомните этот пароль для дальнейшего использования.
5. По завершению установки, PostgreSQL будет автоматически запущен как служба на компьютере.
6. Вы можете использовать командную строку или графический для управления PostgreSQL и создания баз данных. Об этом дальше.
### Установка DBeaver 
1. Перейдите на официальный сайт DBeaver: https://dbeaver.io/download/.
2. Прокрутите страницу вниз до раздела "Community Edition". Найдите и выберите ссылку для загрузки соответствующей версии DBeaver для Windows.
3. Запустите загруженный установочный файл.
4. Следуйте инструкциям установщика, выберите желаемую папку установки и дополнительные настройки.
5. В процессе установки вам могут потребоваться дополнительные компоненты или драйверы, например, для работы с конкретной базой данных. Установщик DBeaver предлагает автоматически загрузить необходимые компоненты.
6. По завершении установки, запустите DBeaver из меню Пуск или используйте ярлык на рабочем столе.
## Для macOS
Установку компонентов PostgreSQL для macOS лучше производить с официальных сайтов.
### Установка PostgreSQL
1. Перейдите на [официальный сайт PostgreSQL](https://www.postgresql.org/download/macosx/).
2. Прокрутите страницу вниз до раздела "PostgreSQL Core Distribution". Выберите ссылку для загрузки соответствующей версии PostgreSQL.
3. Загрузите .dmg файл и откройте его.
4. Запустите пакетный файл установки и следуйте инструкциям установщика.
5. По завершении установки, PostgreSQL будет автоматически запущен как служба на компьютере.
6. Вы можете использовать командную строку или графический интерфейс для управления PostgreSQL и создания баз данных. Об этом ниже.
### Установка DBeaver
1. Перейдите на официальный сайт DBeaver: https://dbeaver.io/download/.
2. Прокрутите страницу вниз до раздела "Community Edition". Найдите и выберите ссылку для загрузки соответствующей версии DBeaver для macOS.
3. Загрузите .dmg файл и откройте его.
4. Перетащите значок DBeaver в папку "Приложения" для установки.
5. После установки, найдите DBeaver в папке "Приложения" и запустите его.


## Для Linux
Для Linux лучше воспользоваться терминалом, это быстрее, но сложнее.
### Установка PostgreSQL
1. Откройте терминал. Например, bash.
2. Выполните следующую команду для установки PostgreSQL с помощью менеджера пакетов в дистрибутиве:
- Для Debian и его производных. Например, Ubuntu:
``` bash
sudo apt-get update
sudo apt-get install postgresql
```
- Для Fedora:
```bash
sudo dnf install postgresql-server
```
- Для CentOS и его производных:
```bash
sudo yum install postgresql-server
```

- Другие дистрибутивы Linux могут использовать свои собственные команды установки пакетов. Проверьте документацию дистрибутива или поищите инструкции для установки PostgreSQL.
3. После установки, PostgreSQL будет автоматически запущен как служба на компьютере.
4. Вы можете использовать командную строку или графический интерфейс для управления PostgreSQL и создания баз данных. Об этом ниже.
### Установка DBeaver
1. Откройте терминал. Например, bash.
2. Выполните следующую команду для установки DBeaver с помощью менеджера пакетов в дистрибутиве:

- Для Debian и его производных. Например, Ubuntu:
```bash
  sudo apt-get update
  sudo apt-get install dbeaver-ce
```
- Для Fedora:
```bash
sudo dnf install dbeaver
```
- Для CentOS и его производных:
```bash
sudo yum install dbeaver-ce
```
- Другие дистрибутивы Linux могут использовать свои собственные команды установки пакетов. Проверьте документацию дистрибутива или поищите инструкции для установки DBeaver.
3. По завершении установки, запустите DBeaver из меню приложений или выполните команду `dbeaver` в терминале.


## Проверяем работу.

После установки и настройки PostgreSQL, можно создавать базы данных, выполнять запросы SQL, управлять таблицами и многое другое. Проверим работу PostgreSQL сделав небольшое практическое задание.

### Само задание
Вы являетесь администратором базы данных в компании и появилась задача создать базу данных для учёта клиентов и их заказов. Нужно создать схему базы данных, таблицы с нужными полями, а также внести несколько записей с данными.
  
1. Создайте базу данных и схемы с помощью DBeaver и SQL. 
  
Решение:
1. Запустите средство управления базами, то есть DBeaver.
2. Создайте новую базу данных, назовите ее "ecommerce":
```sql
CREATE DATABASE ecommerce;
```
3. Переключитесь на созданную базу данных:
```sql
\c ecommerce;
```
4. Создайте новую схему с именем "public":
```sql
CREATE SCHEMA public;
```  

2. Создайте таблицу "customers" для хранения данных о клиентах и "orders" для хранения данных о заказах.

Решение:
  
```sql
   CREATE TABLE public.customers (
     id SERIAL PRIMARY KEY,
     name VARCHAR(100),
     email VARCHAR(100),
     address VARCHAR(200)

);

   CREATE TABLE public.orders (
     id SERIAL PRIMARY KEY,
     customer_id INT,
     product VARCHAR(100),
     quantity INT,
     price NUMERIC(10, 2),
     order_date DATE,
     FOREIGN KEY (customer_id) REFERENCES public.customers (id)
);
```

3. Вставьте несколько записей в таблицы "customers" и  "orders"

Решение:
```sql
INSERT INTO public.customers (name, email, address) 
VALUES ('John Doe', 'johndoe@example.com', '123 Main St'),
       ('Jane Smith', 'janesmith@example.com', '456 Elm St');
   
INSERT INTO public.orders (customer_id, product, quantity, price, order_date)
VALUES (1, 'Product A', 2, 19.99, '2023-10-29'),
       (2, 'Product B', 1, 9.99, '2023-10-30');
```  

 4. Получите все записи из таблиц "customers" и "orders".

```sql
SELECT * FROM public.customers;
SELECT * FROM public.orders;
```

   
## Итоги
Мы успешно установили СУБД PostgreSQL и программу для просмотра баз данных DBeaver. Далее создали базу данных, схему, таблицы и внесли несколько записей с данными. Теперь можно продолжить работу с базой данных, добавлять новые записи, выполнять запросы и выполнять другие операции по мере необходимости.
