### Q : Find all actors who acted in more than one language. Output should contain actor_name, language. Sorted by languages, actor_name.
``` sql
with tb1 as
(select distinct (actor.first_name || ' ' || actor.last_name) as aname,film.language_id
from film
         inner join language
                    on film.language_id = language.language_id
         inner join film_actor
                    on film.film_id = film_actor.film_id
         inner join actor
                    on film_actor.actor_id = actor.actor_id
group by aname , film.language_id
order by aname)
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
order by name
LIMIT 25;
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
order by count(*), film.rental_rate desc
LIMIT 3;
```


### Q : Query to Find Actors Who Have Collaborated the Most.
``` sql
with temptable as
    (select (actor.first_name || ' ' || actor.last_name) as name,
            film_id,
            actor.actor_id
     from actor
              inner join film_actor
                         on actor.actor_id = film_actor.actor_id)

select distinct table1.name as f, table2.name as s, count(*)
from temptable table1
         join temptable table2
              on table1.name > table2.name
where (table1.film_id = table2.film_id and
       table1.actor_id != table2.actor_id)
group by f, s
order by count(*) desc
LIMIT 1;
```

### Q : select the staffs firstname and lastname in one column and their whole payment
``` sql
select (staff.first_name || ' ' || staff.last_name) name,
       sum(payment.amount) as Cost
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
where film.release_year = '2006'
group by category.name
order by count(*) desc
LIMIT 1;
```

### Q : Determine which customer watch how many movies of particular actor.
``` sql
select (customer.first_name || ' ' || customer.last_name) as cname,
       (actor.first_name || ' ' || actor.last_name) as aname,
       count(*)
from film
         inner join film_actor
                    on film.film_id = film_actor.film_id
         inner join actor
                    on film_actor.actor_id = actor.actor_id
         inner join inventory
                    on film.film_id = inventory.film_id
         inner join rental
                    on inventory.inventory_id = rental.inventory_id
         inner join customer
                    on customer.customer_id = rental.customer_id
group by cname,aname
order by count(*) desc;
```

### Q : What is the average rental duration for the top 5 films that have been rented by customers in each country?
``` sql
with films_by_country as(
    select
        country.country,
        film.title as movie,
        film.rental_duration,
        row_number() over (partition by country.country order by count(*) desc) as row
    from film
             inner join inventory on film.film_id = inventory.film_id
             inner join rental on inventory.inventory_id = rental.inventory_id
             inner join customer on rental.customer_id = customer.customer_id
             inner join address on customer.address_id = address.address_id
             inner join city on address.city_id = city.city_id
             inner join country on city.country_id = country.country_id
    group by country.country, movie, film.rental_duration
)
select country, avg(rental_duration)
from films_by_country
where row <= 5
group by country
order by country;
```

### Q :  Find the Location of staff whose inventory are used for making films whose release year is 2005.
``` sql
select address.district, film.film_id
from film
         inner join inventory
                    on film.film_id = inventory.film_id
         inner join rental
                    on inventory.inventory_id = rental.inventory_id
         inner join staff
                    on rental.staff_id = staff.staff_id
        inner join store
    on staff.staff_id = store.manager_staff_id
         inner join address
                    on store.address_id = address.address_id
where film.release_year = 2006;
```

### Q : List out top 10 most revenue generated district to release animated film with average price running on that district
``` sql
select address.district, round(avg(rental_rate), 2)
from film
         inner join film_category
                    on film.film_id = film_category.film_id
         inner join category
                    on film_category.category_id = category.category_id
         inner join inventory
                    on film.film_id = inventory.film_id
         inner join rental
                    on inventory.inventory_id = rental.inventory_id
         inner join payment
                    on rental.rental_id = payment.rental_id
         inner join customer
                    on payment.customer_id = customer.customer_id
         inner join address
                    on customer.address_id = address.address_id
where category.name = 'Animation'
group by address.district
order by sum(amount) desc
LIMIT 10;
```

### Q : list out all films with highest rental rate  and classify the films labelled as "inappropriate for children under 13" with ratings PG-13 , "General" with ratings as G and " Restricted for Age below 18" with ratings as R
``` sql
with tbl as
         (select film.title as movie_name,
                 (case
                      when film.rating = 'PG-13' then 'Inappropriate for children under 13'
                      when film.rating = 'G' then 'General'
                      when film.rating = 'R' then 'Restricted for Age below 18'
                     end) as description
          from film
          order by film.rental_rate desc)

select *
from tbl
where description is not null;
```

### Q : Query to Find Countries with the Longest Average Address Street Length.
``` sql
with tb1 as
         (select country.country as country_name, length(address.address) as len
          from address
                   inner join city
                              on address.city_id = city.city_id
                   inner join country
                              on city.country_id = country.country_id)

select country_name , round(avg(len),2) as average_length
from tb1
group by country_name
order by average_length desc;
```

### Q : Find the Indian Staff whose goods are used in making Hindi films with language id = 1
``` sql
select distinct concat(staff.first_name, ' ', staff.last_name) as staff_name
from address
         inner join staff on address.address_id = staff.address_id
         inner join payment on staff.staff_id = payment.staff_id
         inner join rental on payment.rental_id = rental.rental_id
         inner join inventory on rental.inventory_id = inventory.inventory_id
         inner join film on inventory.film_id = film.film_id
         inner join language on film.language_id = language.language_id
where language.name = 'english'
order by staff_name
limit 500;
```
