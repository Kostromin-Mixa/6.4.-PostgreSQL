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
	SELECT * FROM pg_stats WHERE tablename = 'orders';
	

3.	ALTER TABLE orders RENAME TO orders_old;
	CREATE TABLE public.orders (id integer NOT NULL, title character varying(80) NOT NULL, price integer DEFAULT 0) PARTITION BY RANGE (price);

	CREATE TABLE orders_1 PARTITION OF orders FOR VALUES FROM (499) TO (999999999); 
	CREATE INDEX ON orders_1 (price);

	CREATE TABLE orders_2 PARTITION OF orders FOR VALUES FROM (0) TO (499); 
	CREATE INDEX ON orders_2 (price);

	INSERT INTO orders select * from orders_old;

4.	pg_dump -U postgres test_database > test_database.dump
	92 строчка, после добавления PRIMARY KEY (id) прописать ALTER TABLE orders ADD UNIQUE (title);
	\d+ orders; есть информация уникального значения столбца title
