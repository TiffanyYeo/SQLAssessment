#Task (2)
##What are the Top 25 schools (.edu domains)?
SELECT ROW_NUMBER() OVER 
(
    ORDER BY COUNT(user_id)DESC
) as Rank, email_domain AS "TOP 25 SCHOOLS", COUNT(user_id) AS "Number of Students"
FROM users
GROUP BY email_domain
ORDER BY COUNT(user_id) DESC
LIMIT (25);

##How many .edu learners are located in New York?
SELECT email_domain, city FROM users
WHERE city ="New York";
SELECT count(city) FROM users
WHERE city = "New York";

##The mobile_app column contains either mobile-user or NULL. 
##How many of these Codecademy learners are using the mobile app?
SELECT COUNT(*)
FROM users
WHERE mobile_app = "mobile-user"; 


#Task(3)
SELECT strftime('%H', sign_up_at) AS "By 24 Hours", COUNT(sign_up_at) AS "Number of Sign up"
FROM users
GROUP BY strftime('%H', sign_up_at)
LIMIT 24;


#Task (4):
##Do different schools (.edu domains) prefer different courses?
SELECT count(progress.user_id) AS "Enrolled Students", email_domain AS "School", learn_cpp AS "CPP", learn_sql AS "SQL", learn_html AS "HTML", learn_javascript AS "Javascript", learn_java AS "Java"
FROM users
JOIN progress ON users.user_id = progress.user_id
GROUP BY email_domain
ORDER BY COUNT(progress.user_id) DESC;

##What courses are the New Yorkers students taking?
SELECT users.city, learn_cpp, learn_sql, learn_html, learn_javascript, learn_java 
FROM users
JOIN progress ON users.user_id = progress.user_id
WHERE users.city = "New York";

SELECT users.city, SUM(CASE WHEN learn_cpp != '' THEN 1 ELSE 0 END) AS "Learn CPP",
SUM(CASE WHEN learn_sql != '' THEN 1 ELSE 0 END) AS "Learn SQL", SUM(CASE WHEN learn_html != '' THEN 1 ELSE 0 END) AS "Learn HTML", SUM(CASE WHEN learn_javascript != '' THEN 1 ELSE 0 END) AS "Learn Javascript", SUM(CASE WHEN learn_java != '' THEN 1 ELSE 0 END) AS "Learn JAVA"
FROM users
JOIN progress ON users.user_id = progress.user_id
WHERE users.city = "New York";


##What courses are the Chicago students taking?
SELECT users.city, learn_cpp, learn_sql, learn_html, learn_javascript, learn_java 
FROM users
JOIN progress ON users.user_id = progress.user_id
WHERE users.city = "Chicago";

SELECT users.city, SUM(CASE WHEN learn_cpp != '' THEN 1 ELSE 0 END) AS "Learn CPP",
SUM(CASE WHEN learn_sql != '' THEN 1 ELSE 0 END) AS "Learn SQL", SUM(CASE WHEN learn_html != '' THEN 1 ELSE 0 END) AS "Learn HTML", SUM(CASE WHEN learn_javascript != '' THEN 1 ELSE 0 END) AS "Learn Javascript", SUM(CASE WHEN learn_java != '' THEN 1 ELSE 0 END) AS "Learn JAVA"
FROM users
JOIN progress ON users.user_id = progress.user_id
WHERE users.city = "Chicago";



