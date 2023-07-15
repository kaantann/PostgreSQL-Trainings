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
