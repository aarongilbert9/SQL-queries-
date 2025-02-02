# SQL-queries-
# query to identify the top 10 cities that fall within the top 10 countries 
SELECT C.city, D.country,  
COUNT(A.customer_id) AS customer_count  
FROM customer A  
INNER JOIN address B ON A.address_id = B.address_id  
INNER JOIN city C ON B.city_id = C.city_id  
INNER JOIN country D ON C.country_id = D.country_id  
WHERE D.country IN (  
SELECT D.country  
FROM customer A  
JOIN address B ON A.address_id = B.address_id  
JOIN city C ON B.city_id = C.city_id  
JOIN country D ON C.country_id = D.country_id  
GROUP BY D.country  
ORDER BY COUNT(A.customer_id) DESC  
LIMIT 10)  
GROUP BY C.city, D.country  
ORDER BY customer_count DESC  
LIMIT 10
