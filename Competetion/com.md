### Q : Find all actors who acted in more than one language. Output should contain actor_name, language. Sorted by languages, actor_name.
``` sql
select (actor.first_name || ' ' || actor.last_name) as aname, language.name
from film
         inner join language
                    on film.language_id = language.language_id
         inner join film_actor
                    on film.film_id = film_actor.film_id
         inner join actor
                    on film_actor.actor_id = actor.actor_id
group by aname, language.name
having count(*) > 1
order by language.name, aname;
``` 


### Q : select 25 the actors firstname and lastname in one column named as name and their film names who have released in recent year 2006 order by name
``` sql
select (actor.first_name || ' ' || actor.last_name) as name, film.title
from film
         inner join film_actor
                    on film.film_id = film_actor.film_id
         inner join actor
                    on film_actor.actor_id = actor.actor_id
where film.release_year = 2006
order by name;
```

### Q : List the top 3 actors having done maximum sci-fi movies and with maximum rental rates
``` sql
select (actor.first_name || ' ' || actor.last_name) as aname, category.name, film.rental_rate
from film
         inner join film_category
                    on film.film_id = film_category.film_id
         inner join category
                    on film_category.category_id = category.category_id
         inner join film_actor
                    on film.film_id = film_actor.film_id
         inner join actor
                    on film_actor.actor_id = actor.actor_id
where category.name = 'Sci-Fi'
group by aname, category.name, film.rental_rate
order by count(*), film.rental_rate
LIMIT 3;
```


### Q : Query to Find Actors Who Have Collaborated the Most.
``` sql
select tb1.name as f,
       tb2.name as s,
       count(*)
from (select (a2.first_name || ' ' || a2.last_name) as name,
             film_id,
             a2.actor_id
      from actor as a2
               inner join film_actor f1
                          on a2.actor_id = f1.actor_id) as tb1,
     (select (a1.first_name || ' ' || a1.last_name) as name,
             film_id,
             a1.actor_id
      from actor as a1
               inner join film_actor f2
                          on a1.actor_id = f2.actor_id) as tb2
where (tb1.film_id = tb2.film_id and
       tb1.actor_id != tb2.actor_id)
group by f, s
order by count(*) desc;
```

### Q : select the staffs firstname and lastname in one column and their whole payment
``` sql
select (staff.first_name || ' ' || staff.last_name) name,
       sum(payment.amount) as                       Cost
from staff
         inner join payment
                    on staff.staff_id = payment.staff_id
group by name;
```

### Q : What are the top 10 films that have been rented by customers in the United States, and how many times have they been rented?
``` sql
select film.title, count(*)
from film
         inner join inventory
                    on film.film_id = inventory.film_id
         inner join rental
                    on inventory.inventory_id = rental.inventory_id
         inner join customer
                    on rental.customer_id = customer.customer_id
         inner join address
                    on customer.address_id = address.address_id
         inner join city
                    on address.city_id = city.city_id
         inner join country
                    on city.country_id = country.country_id
where country.country = 'United States'
group by film.title
order by count(*) desc
LIMIT 10;
```


### Q : Find the category which was rented the most for each month in year 2005, if there is a tie find all categories. Sorted by months and category names. Output should contain month, category, count. You can ignore the month if there is no data present for it. 
``` sql
select category.name , count(*)
from film
        inner join film_category
        on film.film_id = film_category.film_id
        inner join category
        on film_category.category_id = category.category_id
         inner join inventory
        on film.film_id = inventory.film_id
         inner join rental
on inventory.inventory_id = rental.inventory_id
group by category.name
order by count(*) desc;
```

### Q : Determine which customer watch how many movies of particular actor.
``` sql
SELECT (customer.first_name || ' ' || customer.last_name) AS CNAME,
       (actor.first_name || ' ' || actor.last_name) AS ANAME,
       count(actor.actor_id)
FROM film
         INNER JOIN film_actor
                    ON film.film_id = film_actor.film_id
         INNER JOIN actor
                    ON film_actor.actor_id = actor.actor_id
         INNER JOIN inventory
                    ON film.film_id = inventory.film_id
         INNER JOIN rental
                    ON inventory.inventory_id = rental.inventory_id
         INNER JOIN customer
                    ON customer.customer_id = rental.customer_id
GROUP BY actor.actor_id,CNAME,ANAME
ORDER BY COUNT(*) DESC;
```
