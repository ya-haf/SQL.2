## Задание 1
Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:
* фамилия и имя сотрудника из этого магазина;
* город нахождения магазина;
* количество пользователей, закреплённых в этом магазине.

**SELECT concat(s.first_name  , ' ', s.last_name) as manager , c.city,  count(c2.customer_id) as customers  
FROM staff s  
JOIN address a  ON s.address_id = a.address_id  
JOIN city c  ON a.city_id = c.city_id  
JOIN store s2 ON s2.store_id = s.store_id  
JOIN customer c2 ON s2.store_id = c2.store_id  
GROUP BY manager, c.city  
HAVING customers > 300**

## Задание 2
Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

**select COUNT(LENGTH)  
from film f  
where LENGTH  > (SELECT AVG(LENGTH) from film f2)**

## Задание 3
Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

**SELECT DATE_FORMAT(p.payment_date, '%Y-%M'), sum(p.amount) , count(p.rental_id)  
FROM payment p  
GROUP BY DATE_FORMAT(p.payment_date, '%Y-%M')  
ORDER BY sum(p.amount) DESC  
LIMIT 1**
