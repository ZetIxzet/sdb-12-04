# Домашнее задание к занятию "`SQL. Часть 2`" - `Воронин Алексей`

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

### Решение

```
SELECT CONCAT(s.first_name, ' ', s.last_name) AS 'Name staff', c.city AS City, COUNT(customer_id) AS 'Total customer'
from staff s
join address a ON s.address_id = a.address_id
join city c ON c.city_id = a.city_id
JOIN customer cust ON cust.store_id = s.store_id
GROUP BY s.first_name, s.last_name, c.city
HAVING COUNT(customer_id) > 300;
```
![Скриншот-1]()

### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

### Решение

```
SELECT COUNT(`length`)
from film
WHERE `length` > (SELECT avg(`length`)FROM film)
```
![Скриншот-2]()

### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

### Решение

```
SELECT sum(amount)as Summa_, DATE_FORMAT(payment_date, '%Y/%M') as Data_, count(rental_id) as Arendy_
FROM payment
GROUP by Data_
ORDER BY sum(amount) DESC
LIMIT 1;
```
![Скриншот-3]():
