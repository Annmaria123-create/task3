# task3
# 📊 Bank Marketing Data Analysis with BigQuery

This project demonstrates how to use SQL in Google BigQuery to analyze the [Bank Marketing Dataset]. It includes examples of creating tables, using SQL `JOINs`, filtering, and extracting insights from the data.

---

## 🗂 Dataset Description

The dataset contains marketing campaign data of a Portuguese banking institution. The marketing campaigns were based on phone calls, and the goal was to predict whether the client would subscribe to a term deposit.

**Source File:** `bankmarketing.csv`

### Key Columns:

- `age`: age of the client
- `job`: type of job
- `marital`: marital status
- `education`: education level
- `default`: has credit in default?
- `housing`: has housing loan?
- `loan`: has personal loan?
- `contact`: contact communication type
- `month`: last contact month
- `day_of_week`: last contact day
- `duration`: last contact duration
- `campaign`: number of contacts during this campaign
- `y`: target variable (has subscribed to a term deposit?)

---

## 🏗 Table Creation in BigQuery
SELECT age, job, y
FROM `imposing-vista-456007-p4.bankmarketing.bank` LIMIT 10
-----
-----
SELECT age, job, y
FROM `imposing-vista-456007-p4.bankmarketing.bank` 
WHERE age > 40
LIMIT 20;
-----
-----
SELECT job, COUNT(*) AS total_yes
FROM `imposing-vista-456007-p4.bankmarketing.bank` 
WHERE job = 'services'
GROUP BY job
ORDER BY total_yes DESC;
-----
-----
SELECT *
FROM `imposing-vista-456007-p4.bankmarketing.bank` 
WHERE job = 'retired'
LIMIT 10;
-----
-----
SELECT age, job, marital, housing
FROM `imposing-vista-456007-p4.bankmarketing.bank` 
WHERE marital = 'married' AND housing = 'yes'
LIMIT 20;
-----
-----
SELECT age, job, education
FROM `imposing-vista-456007-p4.bankmarketing.bank` 
ORDER BY age DESC
LIMIT 10;
-----
-----
SELECT marital, COUNT(*) AS total_clients
FROM `imposing-vista-456007-p4.bankmarketing.bank` 
GROUP BY marital;
----
----
SELECT age, job, education
FROM `imposing-vista-456007-p4.bankmarketing.bank` 
WHERE age < 30 AND job = 'student'
ORDER BY age
limit 20;
-----
-----
SELECT education, AVG(age) AS avg_age
FROM `imposing-vista-456007-p4.bankmarketing.bank` 
GROUP BY education
ORDER BY avg_age DESC;
-----
-----
SELECT job, COUNT(*) AS yes_count
FROM `imposing-vista-456007-p4.bankmarketing.bank` 
WHERE job = 'retired'
GROUP BY job
HAVING COUNT(*) > 100
ORDER BY yes_count DESC;
-----
-----
SELECT age, job, marital, y
FROM `imposing-vista-456007-p4.bankmarketing.bank` 
WHERE age BETWEEN 30 AND 40
limit 20;
-----
-----
SELECT job, COUNT(*) AS married_yes
FROM `imposing-vista-456007-p4.bankmarketing.bank` 
WHERE job = 'blue-collar' AND marital = 'married'
GROUP BY job
HAVING married_yes > 50
ORDER BY married_yes DESC;
-----
-----
SELECT job, COUNT(*) AS married_yes
FROM `imposing-vista-456007-p4.bankmarketing.bank` 
WHERE housing = 'no' AND contact = 'cellular'
GROUP BY job
HAVING married_yes > 50
ORDER BY married_yes DESC;
-----
-----
SELECT age, job, campaign
FROM `imposing-vista-456007-p4.bankmarketing.bank` 
WHERE campaign > (
    SELECT AVG(campaign)
    FROM `imposing-vista-456007-p4.bankmarketing.bank`
)
LIMIT 10;
-----
-----
SELECT *
FROM (
    SELECT job, AVG(campaign) AS avg_campaign
    FROM `imposing-vista-456007-p4.bankmarketing.bank`
    GROUP BY job
) AS job_balances
WHERE avg_campaign > 2.6005747126436773;
-----
-----
SELECT age, education, campaign
FROM imposing-vista-456007-p4.bankmarketing.bank AS b1
WHERE campaign > (
    SELECT AVG(campaign)
    FROM imposing-vista-456007-p4.bankmarketing.bank AS b2
    WHERE b1.education = b2.education
)
LIMIT 20;
----
----
SELECT  
  age,
  job,
  campaign,
  (SELECT AVG(campaign) FROM imposing-vista-456007-p4.bankmarketing.bank ) AS overall_avg_balance
FROM imposing-vista-456007-p4.bankmarketing.bank 
LIMIT 20; 
----
----
SELECT a.*, b.job
FROM `project.dataset.bank_marketing` a
INNER JOIN `project.dataset.other_table` b
ON a.id = b.id
----
----
SELECT a.*, b.job
FROM `project.dataset.bank_marketing` a
LEFT JOIN `project.dataset.other_table` b
ON a.id = b.id
----
----
SELECT a.*, b.job
FROM `project.dataset.bank_marketing` a
RIGHT JOIN `project.dataset.other_table` b
ON a.id = b.id
----
