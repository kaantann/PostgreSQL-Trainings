# PostgreSQL-Trainings
In this repository, I solve challenges that are asked to do in my SQL Course on Udemy. If you would like to learn SQL, I highly recommend this course.
You can directly go to the course page :   `www.udemy.com/course/the-complete-sql-bootcamp/`

This repository only contains solutions of the challenges I faced during the course.

## Q:We want to send out a promotional email to our existing customers.
Answer:
```
SELECT first_name, last_name, email FROM customer;
```

## Q:An Australian visitor isn't familiar with MPAA movie ratings (e.g. PG, PG-13, R, etc..). We want to know the types of ratings we have in our database.
Answer:
```
SELECT DISTINCT rating FROM film;
```

## Q:A customer forgot their wallet at out store! We need to track down their email to inform them. What is the email for the customer with the name Nancy Thomas?
Answer:
```
SELECT email FROM customer
WHERE first_name = 'Nancy' AND last_name = 'Thomas';
```

## Q:A customer wants to know what the movie 'Outlaw Hanky' is about. Could you give them the description for the movide 'Outlaw Hanky'?
Answer:
```
SELECT description from film
WHERE title = 'Outlaw Hanky';
```

## Q:A customer is late on their movie return, and we've mailed them a letter to their address at '259 Ipoh Drive'. We should also call them on the phone to let them know. Can you get the phone number for the customer who lives at '259 Ipoh Drive'?
Answer:
```
SELECT phone FROM address
WHERE address = '259 Ipoh Drive';
```

## Q:We want to reward our first 10 paying customers. What are the customer ids of the first 10 customers who created a payment?
Answer:
```
SELECT customer_id FROM payment
ORDER BY payment_date ASC
LIMIT 10;
```

## Q:A customer wants to quickly rent a video to watch over their short lunch break. What are the titles of the 5 shortest (in length of runtime) movies?
Answer:
```
SELECT title, length FROM film
ORDER BY length ASC
LIMIT 5;
```

## Q:If the previous customer can watch any movie that is 50 minutes or less in run time, how many options does she have?
Answer:
```
SELECT COUNT(title) FROM film
WHERE length <= 50;
```

## Q:How many payment transactions were geater than $5.00?
Answer:
```
SELECT COUNT(amount) FROM payment
WHERE amount > 5;
```

## Q:How many actors have a first name that starts with the letter P?
Answer:
```
SELECT COUNT(*) from actor
WHERE first_name LIKE 'P%';
```

## Q:How many unique districts are our customers from?
Answer:
```
SELECT COUNT(DISTINCT(district)) FROM address;
```

## Q:How many films have a rating of R and a replacement cost between $5 and $15?
Answer:
```
SELECT COUNT(*) FROM film
WHERE rating = 'R' AND replacement_cost BETWEEN 5 AND 15;
```

## Q:How many films have the word Truman somewhere in the title?
Answer:
```
SELECT COUNT(*) FROM film
WHERE title LIKE '%Truman%';
```

## Q: We have two staff members, with Staff IDs 1 and 2. We want to give a bonus to the staff member that handled the most payments (Most in terms of number of payments processes, not total dollar amount.). How many payments did each staff member handle and who gets the bonus?
Answer:
```
SELECT staff_id, COUNT(amount) FROM payment
GROUP BY staff_id;
```

## Q: Corporate HQ is conducting a study on the relationship between replacement cost and a movie MPAA rating. What is the average replacement cost per MPAA rating?
Answer:
```
SELECT rating, ROUND(AVG(replacement_cost),2) FROM film
GROUP BY rating;
```

## Q: We are running a promotion to reward our top 5 customers with coupons. What are the customer ids of the top 5 customers by total spend?
Answer:
```
SELECT customer_id, SUM(amount) FROM payment
GROUP BY customer_id
ORDER BY SUM(amount) DESC
LIMIT 5;
```

## Q: We are launching a platinum service for our most loyal customers. We will assign platinum status to customers that have had 40 or more transaction payments. What customer_ids are eligible for platinum status?
Answer:
```
SELECT customer_id, COUNT(amount) FROM payment
GROUP BY customer_id
HAVING COUNT(amount) >= 40;
```

## Q: What are the customer ids of customers who have spent more than $100 in payment transactions with our staff_id member 2?
Answer:
```
SELECT customer_id, staff_id, SUM(amount) FROM payment
GROUP BY staff_id, customer_id
HAVING  SUM(amount) > 100 AND staff_id = 2;
```

but, a better solution could be this:

```
SELECT customer_id, SUM(amount) FROM payment
WHERE staff_id = 2
GROUP BY customer_id
HAVING SUM(amount) > 100;
```

# Assesment Test 1
## Q: Return the customer IDs of customers who have spent at least $110 with the staff member who has an ID of 2
Answer:
```
SELECT customer_id, SUM(amount) FROM payment
WHERE staff_id = 2
GROUP BY customer_id
HAVING SUM(amount) > 110;
```

## Q: How many films begin with the letter J?
Answer:
```
SELECT COUNT(*) FROM film
WHERE title ILIKE 'J%';
```

## Q: What customer has the highest customer ID number whose name starts with an 'E' and has an address ID lower than 500?
Answer:
```
SELECT first_name, last_name FROM customer
WHERE first_name ILIKE 'E%' AND address_id < 500 
ORDER BY customer_id DESC
LIMIT 1;
```

## Q: California sales tax laws have changed and we need to alert our customers to this through email. What are the emials of customers who live in California?
Answer:
```
SELECT customer.email,district FROM address
INNER JOIN customer
ON customer.address_id = address.address_id
WHERE district = 'California'
```

## Q: A customer walks in and is a huge fan of the actor "Nick Wahlberg" and wants to know which movies he is in. Get a list of all the movies "Nick Wahlberg" has been in.
Answer:
```
SELECT title FROM film
INNER JOIN film_actor
ON film.film_id = film_actor.film_id
WHERE actor_id = 2
```
In this case, Nick Wahlberg's id was assigned to 2. I believe that I should select the id first (since actor id could be change in time), but I do not know how to do multiple querying and storing as a variable to use it later. So, it is a bit dirty code imho.

PS: I learnt that actor_id could be retrieved using a second inner join, but I think there could be some other way to do it. Using a second inner join could overload the system , and that situation is not very welcomed imo.

## Q: During which months did payments occur? Format your answer to return back the full month name.
Answer:
```
SELECT DISTINCT(TO_CHAR(payment_date,'MONTH'))
FROM payment;
```

## Q: How many payments occured on Monday?
Answer:
```
SELECT COUNT(*) FROM payment
WHERE EXTRACT(dow FROM payment_date) = 1;
```

## Q: How can you retrieve all the information from the cd.facilities table?
Answer:
```
SELECT * FROM cd.facilities;
```

## Q: You want to print out a list of all of the facilities and their cost to members. How would you retrieve a list of only facility names and costs?
Answer:
```
SELECT name,membercost FROM cd.facilities;
```

## Q: How can you produce a list of facilities that charge a fee to members?
Answer:
```
SELECT * FROM cd.facilities
WHERE membercost != 0;
```

## Q: How can you produce a list of facilities that charge a fee to members, and that fee is less than 1/50th of the monthly maintenance cost? Return the facid, facility name, member cost, and monthly maintenance of the facilities in question.
Answer:
```
SELECT facid, name, membercost,monthlymaintenance FROM cd.facilities
WHERE membercost != 0 AND membercost < monthlymaintenance / 50;
```

## Q: How can you produce a list of all facilities with the word 'Tennis' in their name?
Answer:
```
SELECT * FROM cd.facilities
WHERE name LIKE '%Tennis%';
```

## Q: How can you retrieve the details of facilities with ID 1 and 5? Try to do it without using the OR operator.
Answer:
```
SELECT * FROM cd.facilities
WHERE MOD(facid,4) = 1
```

PS: I did not understand the reasoning why we do not use OR operator. Since I got the right solution, I won't change it for now. However, after checking the solutions, may be I get purpose of the question.

## Q: How can you produce a list of members who joined after the start of September 2012? Return the memid, surname, firstname, and joindate of the members in question.
Answer:
```

```
