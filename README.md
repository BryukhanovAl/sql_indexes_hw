# Домашнее задание к занятию «Индексы»

### Задание 1
Напишите запрос к учебной базе данных, который вернёт процентное отношение общего размера всех индексов к общему размеру всех таблиц.

SELECT table_schema, sum(index_length / data_length) * 100 "Size in %"
FROM information_schema.TABLES
GROUP BY table_schema
HAVING table_schema = "sakila";

### Задание 2
Выполните explain analyze следующего запроса:
- перечислите узкие места;
Избыточные запросы к таблицам, которые не нужны для получения этих данных, в оконной функции лишняя таблица, лишние условия.

- оптимизируйте запрос: внесите корректировки по использованию операторов, при необходимости добавьте индексы.

select distinct concat(c.last_name, ' ', c.first_name), sum(p.amount), p.payment_date 
from payment p
join customer c on c.customer_id = p.customer_id
join rental r on r.rental_id = p.rental_id
group by p.payment_id 
having p.payment_date >= '2005-07-30' and p.payment_date < date_add('2005-07-30', INTERVAL 1 DAY);

------------------------------------------------------------------------------------------------------------------------

explain analyze
select distinct concat(c.last_name, ' ', c.first_name), sum(p.amount), p.payment_date 
from payment p
join customer c on c.customer_id = p.customer_id
join rental r on r.rental_id = p.rental_id
group by p.payment_id 
having p.payment_date >= '2005-07-30' and p.payment_date < date_add('2005-07-30', INTERVAL 1 DAY);

![sql_indexes_hw_task2](https://github.com/EvgenyMyznikov/sql_indexes_hw/blob/main/img/Task2.png?raw=true)
