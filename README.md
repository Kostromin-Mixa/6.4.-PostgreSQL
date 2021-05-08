# 6.4.-PostgreSQL
1.	docker pull postgres:13
	docker run --name my-postgr13 -e POSTGRES_PASSWORD=1234 -d -p 5432:5432 -v /postgres/base:/var/lib/postgresql/data postgres:13
	docker exec -it my-postgr13 bash
	psql -U postgres
Команды \? :
	\list - выводит все базы
	\connect - подключает к нужной базе
	\dt - выводит список всех даблиц
	\d+ - выводит описание таблицы
	\q - выход из psql

2.	CREATE DATABASE test_database;
	psql -U postgres test_database < test_dump.sql
	psql -U postgres
	\connect test_database;
	\dt
	ANALYZE orders;
	

3.	CREATE TABLE orders_1 ( CHECK ( price > 499 )) INHERITS (orders);
	CREATE RULE orders_insert_1 AS ON INSERT TO orders WHERE ( price > 499 ) DO INSTEAD INSERT INTO orders_1 VALUES (NEW.*);
	CREATE TABLE orders_2 ( CHECK ( price <= 499 )) INHERITS (orders);
	CREATE RULE orders_insert_2 AS ON INSERT TO orders WHERE ( price <= 499 ) DO INSTEAD INSERT INTO orders_2 VALUES (NEW.*);

4.	pg_dump -U postgres test_database > test_database2.dump
