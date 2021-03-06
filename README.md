# SQL for Yelp Dataset
Using SQL for Analysing Yelp dataset on a Coursera's online course with name of SQL for Data Science.

### by Hamed Davoudabadi

In this assignment, specifically, I was going to be playing the role of a real-world data scientist using SQL to both answer specific questions for an organization and make inferences based on my discoveries. 

I will be using a dataset from a US-based organization called Yelp, which provides a platform for users to provide reviews and rate their interactions with a variety of organizations, businesses, restaurants, health clubs, hospitals, local governmental offices, charitable organizations, etc. Yelp has made a portion of this data available for personal, educational, and academic purposes.

I was asked a series of questions regarding the data to help me profile and better understand the data in the first part of the assignment. Also, there are some questions in part 2, which require writing a variety of SQL statements.

## Scenario
**Data Scientist Role Play**: Profiling and Analyzing the Yelp Dataset Coursera Worksheet

This is a 2-part assignment. In the first part, you are asked a series of questions that will help you profile and understand the data just like a data scientist would. For this first part of the assignment, you will be assessed both on the correctness of your findings, as well as the code you used to arrive at your answer. You will be graded on how easy your code is to read, so remember to use proper formatting and comments where necessary.

In the second part of the assignment, you are asked to come up with your own inferences and analysis of the data for a particular research question you want to answer. You will be required to prepare the dataset for the analysis you choose to do. As with the first part, you will be graded, in part, on how easy your code is to read, so use proper formatting and comments to illustrate and communicate your intent as required.

For both parts of this assignment, use this "worksheet." It provides all the questions you are being asked, and your job will be to transfer your answers and SQL coding where indicated into this worksheet so that your peers can review your work. You should be able to use any Text Editor (Windows Notepad, Apple TextEdit, Notepad ++, Sublime Text, etc.) to copy and paste your answers. If you are going to use Word or some other page layout application, just be careful to make sure your answers and code are lined appropriately. In this case, you may want to save as a PDF to ensure your formatting remains intact for you reviewer.

**ER Diagram**:

All of the questions in this project refer to the open source **Chinook Database**. This diagram is going to help us in order to familiarize ourself with the table and column names for writing accurate queries and getting the appropriate answers.

![image](https://ucde-rey.s3.amazonaws.com/DSV1015/ChinookDatabaseSchema.png "Chinook Database ER Diagram")

## Part 1: Yelp Dataset Profiling and Understanding

#### 1) Profile the data by finding the total number of records for each of the tables below:
```	
i. Attribute table  = 	10,000
ii. Business table  = 	10,000
iii. Category table = 	10,000
iv. Checkin table   = 	10,000
v. elite_years table =  10,000
vi. friend table    = 	10,000
vii. hours table    = 	10,000
viii. photo table   = 	10,000
ix. review table    = 	10,000 
x. tip table        = 	10,000
xi. user table      = 	10,000
```	

#### 2) Find the total number of distinct records for the primary keys in each of the tables listed below:
```
i. Business     = 	10000
ii. Hours       = 	1562
iii. Category   = 	2643
iv. Attribute   = 	1115
v. Review       = 	10000
vi. Checkin     = 	493
vii. Photo      = 	10000
viii. Tip       = 	537 
ix. User        = 	10000
x. Friend       = 	11
xi. Elite_years = 	2780
```
Note: Primary Keys are denoted in the ER-Diagram with a yellow key icon.	

#### 3) Are there any columns with null values in the Users table? Indicate "yes," or "no."

Answer: NO

SQL code used to arrive at answer:	

1st Way:
```
	SELECT
 	count(*)
	FROM user
	WHERE id IS NULL
```	
Way 2nd:
```
        SELECT id, 
        CASE 
            WHEN 
                id IS NULL
                OR name IS NULL
                OR review_count IS NULL
                OR yelping_since IS NULL
                OR useful IS NULL
                OR funny IS NULL
                OR cool IS NULL
                OR fans IS NULL
                OR average_stars IS NULL
                OR compliment_hot IS NULL
                OR compliment_more IS NULL
                OR compliment_profile IS NULL
                OR compliment_cute IS NULL
                OR compliment_note IS NULL
                OR compliment_plain IS NULL
                OR compliment_cool IS NULL
                OR compliment_funny IS NULL
                OR compliment_writer IS NULL
                OR compliment_photos IS NULL
            THEN 1
            ELSE 0
        END AS Nulls
        FROM user
        WHERE Nulls = 1;
```
Result:
>        +-------+
>        | Nulls |
>        +-------+
>        +-------+
>        (Zero rows)
	
#### 4) For each table and column listed below, display the smallest (minimum), largest (maximum), and average (mean) value for the following fields:

i. Table: Review, Column: Stars
	
> min: 1, max: 5, avg: 3.7082

Code:
```
SELECT count(stars) , min(stars) as minim, max(stars) as maxim, avg(stars) as average
FROM review 
```
Result:
>		+--------------+-------+-------+---------+
>		| count(stars) | minim | maxim | average |
>		+--------------+-------+-------+---------+
>		|        10000 |     1 |     5 |  3.7082 |
>		+--------------+-------+-------+---------+		
	
ii. Table: Business, Column: Stars
	
> min: 1, max: 5, avg: 3.6549
		
	
iii. Table: Tip, Column: Likes
	
> min: 0, max: 2, avg: 0.0144
		
	
iv. Table: Checkin, Column: Count
	
> min: 1, max: 53, avg: 1.9414
		
	
v. Table: User, Column: Review_count
	
> min: 0, max: 2,000, avg: 24.2995
		

#### 5) List the cities with the most reviews in descending order:

SQL code used to arrive at answer:
```       
		SELECT City, sum(review_count) as Number_of_Reviews
		FROM business
		GROUP BY City
		ORDER BY Number_of_Reviews DESC
```	
Result:
```
+-----------------+-------------------+
| city            | Number_of_Reviews |
+-----------------+-------------------+
| Las Vegas       |             82854 |
| Phoenix         |             34503 |
| Toronto         |             24113 |
| Scottsdale      |             20614 |
| Charlotte       |             12523 |
| Henderson       |             10871 |
| Tempe           |             10504 |
| Pittsburgh      |              9798 |
| Montr??al        |              9448 |
| Chandler        |              8112 |
| Mesa            |              6875 |
| Gilbert         |              6380 |
| Cleveland       |              5593 |
| Madison         |              5265 |
| Glendale        |              4406 |
| Mississauga     |              3814 |
| Edinburgh       |              2792 |
| Peoria          |              2624 |
| North Las Vegas |              2438 |
| Markham         |              2352 |
| Champaign       |              2029 |
| Stuttgart       |              1849 |
| Surprise        |              1520 |
| Lakewood        |              1465 |
| Goodyear        |              1155 |
+-----------------+-------------------+
(Output limit exceeded, 25 of 362 total rows shown)
```
	
#### 6) Find the distribution of star ratings to the business in the following cities:

i. Avon

SQL code used to arrive at answer:
```
	SELECT count(*) as Num_Stars, stars
	FROM business
        WHERE city = 'Avon'
	GROUP BY stars
```
Result:
```
+-----------+-------+
| Num_Stars | stars |
+-----------+-------+
|         1 |   1.5 |
|         2 |   2.5 |
|         3 |   3.5 |
|         2 |   4.0 |
|         1 |   4.5 |
|         1 |   5.0 |
+-----------+-------+
```
ii. Beachwood

SQL code:
```	
	SELECT count(*) as Num_Stars, stars
	FROM business
        WHERE city = 'Beachwood'
	GROUP BY stars
```
Result:
```
+-----------+-------+
| Num_Stars | stars |
+-----------+-------+
|         1 |   2.0 |
|         1 |   2.5 |
|         2 |   3.0 |
|         2 |   3.5 |
|         1 |   4.0 |
|         2 |   4.5 |
|         5 |   5.0 |
+-----------+-------+
```

#### 7) Find the top 3 users based on their total number of reviews:
		
SQL Code:
```
	SELECT name, yelping_since, review_count
	FROM user
	GROUP BY review_count
	ORDER BY review_count DESC
	limit 3
```		
Result:
```
+--------+---------------------+--------------+
| name   | yelping_since       | review_count |
+--------+---------------------+--------------+
| Gerald | 2012-12-16 00:00:00 |         2000 |
| Sara   | 2010-05-16 00:00:00 |         1629 |
| Yuri   | 2008-01-03 00:00:00 |         1339 |
+--------+---------------------+--------------+	
```

#### 8) Does posing more reviews correlate with more fans?

Please explain your findings and interpretation of the results: 

With growing the number of reviews for each person, his fans does not increase. So, it means that there is no correlation between review count and number of fans. Top 10 persons with most reviews and their fans number has been shown in the below:
```
+-----------+---------------------+--------------+------+
| name      | yelping_since       | review_count | fans |
+-----------+---------------------+--------------+------+
| Gerald    | 2012-12-16 00:00:00 |         2000 |  253 |
| Sara      | 2010-05-16 00:00:00 |         1629 |   50 |
| Yuri      | 2008-01-03 00:00:00 |         1339 |   76 |
| .Hon      | 2006-07-19 00:00:00 |         1246 |  101 |
| William   | 2015-02-19 00:00:00 |         1215 |  126 |
| Harald    | 2012-11-27 00:00:00 |         1153 |  311 |
| eric      | 2007-05-27 00:00:00 |         1116 |   16 |
| Roanna    | 2006-03-28 00:00:00 |         1039 |  104 |
| Mimi      | 2011-03-30 00:00:00 |          968 |  497 |
| Christine | 2009-07-08 00:00:00 |          930 |  173 |
+-----------+---------------------+--------------+------+
```
There is another way which is more scientific for answering this question. We can create the distribution for average of reviews and number of fans. With this way you can see that reviews are positively correlated with fans.
	
For using the 2nd way, we should utilize Case statement to bin fans into 5 categories incrementally, then find the average reviews of each bin. If the two are correlated, you will expect the review numbers to increase as the fan_bin increases.
```
   SELECT
       CASE
           WHEN fans < 10 THEN 1
           WHEN fans < 20 THEN 2
           WHEN fans < 30 THEN 3
           WHEN fans < 40 THEN 4
           ELSE 5
       END AS fans_bin, 
	   AVG(review_count) AS avg_reviews
   FROM user
   GROUP BY fans_bin
   ORDER BY fans_bin;
```
Result:
```
+----------+---------------+
| fans_bin |   avg_reviews |
+----------+---------------+
|        1 | 15.0085655315 |
|        2 | 225.058441558 |
|        3 | 281.821428571 |
|        4 | 377.161290323 |
|        5 | 513.463768116 |
+----------+---------------+
```
#### 9) Are there more reviews with the word "love" or with the word "hate" in them?

Answer: The reviews with love are almost 8 times the number of words with hate: 
*Hate= 232*
*Love= 1,780*
	
SQL Code:
```
	SELECT SUM(LOVE) AS Love, 
               SUM(HATE) AS Hate 
	FROM
	      (SELECT (text LIKE "%love%") AS LOVE, 
              (text LIKE "%hate%") AS HATE 
	       FROM Review)
```
	
#### 10) Find the top 10 users with the most fans:

SQL Code:
```	
	SELECT name, yelping_since, fans
	FROM user
	GROUP BY fans
	ORDER BY fans DESC
	Limit 10
```	
Result:
```
+-----------+---------------------+------+
| name      | yelping_since       | fans |
+-----------+---------------------+------+
| Amy       | 2007-07-19 00:00:00 |  503 |
| Mimi      | 2011-03-30 00:00:00 |  497 |
| Harald    | 2012-11-27 00:00:00 |  311 |
| Gerald    | 2012-12-16 00:00:00 |  253 |
| Christine | 2009-07-08 00:00:00 |  173 |
| Lisa      | 2009-10-05 00:00:00 |  159 |
| Cat       | 2009-02-05 00:00:00 |  133 |
| William   | 2015-02-19 00:00:00 |  126 |
| Fran      | 2012-04-05 00:00:00 |  124 |
| Lissa     | 2007-08-14 00:00:00 |  120 |
+-----------+---------------------+------+
```	
#### 11) Is there a strong relationship (or correlation) between having a high number of fans and being listed as "useful" or "funny?" Out of the top 10 users with the highest number of fans, what percent are also listed as ???useful??? or ???funny????

Key:
0% - 25% - Low relationship
26% - 75% - Medium relationship
76% - 100% - Strong relationship
	
SQL Code:
```
	SELECT name, id, fans, useful, funny
	FROM user
	GROUP BY fans
	ORDER BY fans DESC
        Limit 10
```
Result:
```
+-----------+------+--------+--------+
| name      | fans | useful |  funny |
+-----------+------+--------+--------+
| Amy       |  503 |   3226 |   2554 |
| Mimi      |  497 |    257 |    138 |
| Harald    |  311 | 122921 | 122419 |
| Gerald    |  253 |  17524 |   2324 |
| Christine |  173 |   4834 |   6646 |
| Lisa      |  159 |     48 |     13 |
| Cat       |  133 |   1062 |    672 |
| William   |  126 |   9363 |   9361 |
| Fran      |  124 |   9851 |   7606 |
| Lissa     |  120 |    455 |    150 |
+-----------+------+--------+--------+
```
Please explain your findings and interpretation of the results:
*There is a person with name of Harald who has the highest numbers in "useful" and "funny" columns, but his number of fans is 311 which is not the highest number in fans. 
So, with considering the numbers for three columns we can see that there is no correlation between fan number and being labled as funny or useful. *
		

## Part 2: Inferences and Analysis

#### 12) Pick one city and category of your choice and group the businesses in that city or category by their overall star rating. Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions. Include your code.
	
i. Do the two groups you chose to analyze have a different distribution of hours?
Yes they seem to have a different distribution of hours, 2-3 stars are normally around 8:00 to 20:00 while 4-5 stars are mainly between 11:00-21:00.

ii. Do the two groups you chose to analyze have a different number of reviews?
Yes, The review counts for 2-3 stars are much lower than 4-5 stars.         
         
iii. Are you able to infer anything from the location data provided between these two groups? Explain.
Yes, they are so close to each other.

SQL Code:
```
	Select *, 
	CASE  
	WHEN (StarReviews >= 2) AND (StarReviews <= 3) THEN '2-3 Stars'
	WHEN (StarReviews >= 4) AND (StarReviews <= 5) THEN '4-5 Stars'
	ELSE 'Other'
	END ClassByReview
	FROM
	(Select category, COUNT(*) AS Ct,avg(stars) As StarReviews, hours FROm
	business JOIN category
	on business.id = category.business_id
	JOIN hours
	on business.id = hours.business_id
	WHERE CITY = "Toronto"
	GROUP BY category)
	ORDER BY ClassByReview
```
RESULTS:
```
+----------------------+----+-------------+----------------------+---------------+
| category             | Ct | StarReviews | hours                | ClassByReview |
+----------------------+----+-------------+----------------------+---------------+
| Burgers              |  7 |         3.0 | Saturday|10:30-21:00 | 2-3 Stars     |
| Grocery              |  7 |         2.5 | Saturday|8:00-22:00  | 2-3 Stars     |
| Gyms                 |  7 |         3.0 | Saturday|8:00-20:00  | 2-3 Stars     |
| Pizza                |  7 |         3.0 | Saturday|10:00-4:00  | 2-3 Stars     |
| Poutineries          |  7 |         3.0 | Saturday|10:30-21:00 | 2-3 Stars     |
| Yoga                 |  7 |         3.0 | Saturday|8:00-20:00  | 2-3 Stars     |
| Acupuncture          |  7 |         4.5 | Saturday|10:00-14:00 | 4-5 Stars     |
| Arcades              |  7 |         4.5 | Saturday|16:00-2:00  | 4-5 Stars     |
| Art Galleries        |  7 |         4.5 | Saturday|16:00-2:00  | 4-5 Stars     |
| Arts & Entertainment |  7 |         4.5 | Saturday|16:00-2:00  | 4-5 Stars     |
| Beauty & Spas        |  3 |         4.5 | Monday|11:30-18:00   | 4-5 Stars     |
| Beer                 |  6 |         4.0 | Saturday|11:00-21:00 | 4-5 Stars     |
| Books                |  7 |         4.5 | Saturday|16:00-2:00  | 4-5 Stars     |
| Breweries            |  6 |         4.0 | Saturday|11:00-21:00 | 4-5 Stars     |
| Cafes                |  7 |         4.5 | Saturday|16:00-2:00  | 4-5 Stars     |
| Coffee & Tea         |  7 |         4.5 | Saturday|16:00-2:00  | 4-5 Stars     |
| Eyelash Service      |  3 |         4.5 | Monday|11:30-18:00   | 4-5 Stars     |
| Fashion              |  6 |         4.5 | Saturday|11:00-17:00 | 4-5 Stars     |
| French               |  5 |         4.0 | Saturday|18:00-23:00 | 4-5 Stars     |
| Health & Medical     |  7 |         4.5 | Saturday|10:00-14:00 | 4-5 Stars     |
| Korean               |  7 |         4.5 | Saturday|11:00-23:00 | 4-5 Stars     |
| Mags                 |  7 |         4.5 | Saturday|16:00-2:00  | 4-5 Stars     |
| Makeup Artists       |  3 |         4.5 | Monday|11:30-18:00   | 4-5 Stars     |
| Martial Arts         |  5 |         5.0 | Monday|17:00-22:00   | 4-5 Stars     |
| Music & Video        |  7 |         4.5 | Saturday|16:00-2:00  | 4-5 Stars     |
+----------------------+----+-------------+----------------------+---------------+
(Output limit exceeded, 25 of 46 total rows shown)
```
We can also write another query for consideration of number of reviews and the rating (stars), which conclude that the 
business with higher rating have more reviews.
```
SELECT 
-- Get two categories using case, filter out 0 in where clause
    CASE
        WHEN stars BETWEEN 2 AND 3 THEN '2-3'
        WHEN stars BETWEEN 4 and 5 THEN '4-5'
        ELSE '0'
    END AS star_rating,
    review_count,
    city,
    postal_code, 
    category,
    name,
-- Using length to split the hours string into the day of the week, opening time and closing time.
    substr(hours, 0, length(hours)-10) AS day_of_week,
    substr(hours, length(hours)-9, 4) AS open_time,
    substr(hours, length(hours)-4) AS close_time
FROM business AS B
JOIN category AS C ON B.id = C.business_id
JOIN hours AS H ON B.id = H.business_id
WHERE 
    star_rating != '0'
    AND category = 'Shopping'
    AND city = 'Las Vegas';
```	
Result:
```
+-------------+--------------+-----------+-------------+----------+--------------------------------+-------------+-----------+------------+
| star_rating | review_count | city      | postal_code | category | name                           | day_of_week | open_time | close_time |
+-------------+--------------+-----------+-------------+----------+--------------------------------+-------------+-----------+------------+
| 4-5         |           32 | Las Vegas | 89161       | Shopping | Red Rock Canyon Visitor Center | Monday      | 8:00      | 16:30      |
| 4-5         |           32 | Las Vegas | 89161       | Shopping | Red Rock Canyon Visitor Center | Tuesday     | 8:00      | 16:30      |
| 4-5         |           32 | Las Vegas | 89161       | Shopping | Red Rock Canyon Visitor Center | Friday      | 8:00      | 16:30      |
| 4-5         |           32 | Las Vegas | 89161       | Shopping | Red Rock Canyon Visitor Center | Wednesday   | 8:00      | 16:30      |
| 4-5         |           32 | Las Vegas | 89161       | Shopping | Red Rock Canyon Visitor Center | Thursday    | 8:00      | 16:30      |
| 4-5         |           32 | Las Vegas | 89161       | Shopping | Red Rock Canyon Visitor Center | Sunday      | 8:00      | 16:30      |
| 4-5         |           32 | Las Vegas | 89161       | Shopping | Red Rock Canyon Visitor Center | Saturday    | 8:00      | 16:30      |
| 2-3         |            6 | Las Vegas | 89121       | Shopping | Walgreens                      | Monday      | 8:00      | 22:00      |
| 2-3         |            6 | Las Vegas | 89121       | Shopping | Walgreens                      | Tuesday     | 8:00      | 22:00      |
| 2-3         |            6 | Las Vegas | 89121       | Shopping | Walgreens                      | Friday      | 8:00      | 22:00      |
| 2-3         |            6 | Las Vegas | 89121       | Shopping | Walgreens                      | Wednesday   | 8:00      | 22:00      |
| 2-3         |            6 | Las Vegas | 89121       | Shopping | Walgreens                      | Thursday    | 8:00      | 22:00      |
| 2-3         |            6 | Las Vegas | 89121       | Shopping | Walgreens                      | Sunday      | 8:00      | 22:00      |
| 2-3         |            6 | Las Vegas | 89121       | Shopping | Walgreens                      | Saturday    | 8:00      | 22:00      |
| 4-5         |            4 | Las Vegas | 89118       | Shopping | Desert Medical Equipment       | Friday      | 8:00      | 17:00      |
| 4-5         |            4 | Las Vegas | 89118       | Shopping | Desert Medical Equipment       | Tuesday     | 8:00      | 17:00      |
| 4-5         |            4 | Las Vegas | 89118       | Shopping | Desert Medical Equipment       | Thursday    | 8:00      | 17:00      |
| 4-5         |            4 | Las Vegas | 89118       | Shopping | Desert Medical Equipment       | Wednesday   | 8:00      | 17:00      |
| 4-5         |            4 | Las Vegas | 89118       | Shopping | Desert Medical Equipment       | Monday      | 8:00      | 17:00      |
+-------------+--------------+-----------+-------------+----------+--------------------------------+-------------+-----------+------------+
```
#### 13) Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.
		
i. Difference 1:
Average Number of reviews for Closed Business is 23.2 and for open ones is 31.75 (Based on Number of Reviews)
         
ii. Difference 2:
Type of the business are different (based on names, the ones which are not open are a Bistro and a Cafe)
         
SQL Code:
```
	Select  is_open, COUNT(*) AS NoBusiness, AVG(stars) As AverageRating, MAX(stars) As MaxRating, Min(stars) As MinRating, SUM(review_count) AS TotalReviews, AVG(review_count) AS AverageReviews
	FROM Business
	GROUP BY is_open
```
Result:
```
+---------+------------+---------------+-----------+-----------+--------------+----------------+
| is_open | NoBusiness | AverageRating | MaxRating | MinRating | TotalReviews | AverageReviews |
+---------+------------+---------------+-----------+-----------+--------------+----------------+
|       0 |       1520 | 3.52039473684 |       5.0 |       1.0 |        35261 |  23.1980263158 |
|       1 |       8480 | 3.67900943396 |       5.0 |       1.0 |       269300 |  31.7570754717 |
+---------+------------+---------------+-----------+-----------+--------------+----------------+
```	
iii. Difference 3: Businesses with is_open, are more likely to be a nightlife business like bars or restaurants.
SQL Code:
```
SELECT C.category, 
COUNT(B.id) AS total_businesses, 
SUM(CAST(is_open AS real))/CAST(COUNT(B.id) AS real) AS percent_open
FROM business AS B 
JOIN category AS C ON B.id = C.business_id
GROUP BY C.category
ORDER BY total_businesses DESC;
```
Result:
```
+---------------------------+------------------+----------------+
| category                  | total_businesses |   percent_open |
+---------------------------+------------------+----------------+
| Restaurants               |               71 | 0.746478873239 |
| Shopping                  |               30 | 0.833333333333 |
| Food                      |               23 | 0.869565217391 |
| Nightlife                 |               20 |            0.6 |
| Bars                      |               17 | 0.647058823529 |
| Health & Medical          |               17 | 0.941176470588 |
| Home Services             |               16 |         0.9375 |
| Beauty & Spas             |               13 | 0.923076923077 |
| Local Services            |               12 | 0.833333333333 |
| American (Traditional)    |               11 | 0.727272727273 |
| Active Life               |               10 |            1.0 |
| Automotive                |                9 |            1.0 |
| Hotels & Travel           |                9 | 0.888888888889 |
| Burgers                   |                8 |          0.875 |
| Sandwiches                |                8 |           0.75 |
| Arts & Entertainment      |                7 |            1.0 |
| Fast Food                 |                7 |            1.0 |
| Mexican                   |                7 | 0.714285714286 |
| American (New)            |                6 |            0.5 |
| Event Planning & Services |                6 |            0.5 |
| Hair Salons               |                6 |            1.0 |
| Bakeries                  |                5 |            0.8 |
| Doctors                   |                5 |            1.0 |
| Indian                    |                5 |            0.8 |
| Japanese                  |                5 |            0.6 |
+---------------------------+------------------+----------------+
(Output limit exceeded, 25 of 257 total rows shown)
```
	
#### 14) For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.

Ideas for analysis include: Parsing out keywords and business attributes for sentiment analysis, clustering businesses to find commonalities or anomalies between them, predicting the overall star rating for a business, predicting the number of fans a user will have, and so on. These are just a few examples to get you started, so feel free to be creative and come up with your own problem you want to solve. Provide answers, in-line, to all of the following:
	
	
i. Indicate the type of analysis you chose to do:

I can analyse the type of business based on the "name" column, and decide which business is has more fans and reviews. Also, it is important to see Which type of businesses are thriving by reviews and have at least 10 of such.       
       
       
ii. Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:

I would need a column/variable which indicates the type of business. With that information I could recognize for each business what factors are important? For example is the the location of a restaurant important in the stars it gets? I would also check the relation between the type of a business and the number of reviews. Being open or not would be also important for rating in some types of businesses.    
Also, it is possible to compare the restaurants from their type of foods. For example, in query 3 I have tried to make different type of restaurants and check the ratings for each category of foods.
 
iii. SQL codes and Results:

Query 1:
```
SELECT name, b.city, c.category, b.stars, b.review_count, b.is_open 
FROM business b 
LEFT JOIN category c
ON b.id = c.business_id
where b.city like '%Vegas%' and c.category is not null
ORDER BY c.category DESC
```
Result:
```
+------------------------------------------------+-----------+-------------------------------+-------+--------------+---------+
| name                                           | city      | category                      | stars | review_count | is_open |
+------------------------------------------------+-----------+-------------------------------+-------+--------------+---------+
| Red Rock Canyon Visitor Center                 | Las Vegas | Visitor Centers               |   4.5 |           32 |       1 |
| Jacques Cafe                                   | Las Vegas | Vegetarian                    |   4.0 |          168 |       0 |
| WorldMark Las Vegas - Spencer Street           | Las Vegas | Vacation Rentals              |   3.5 |           19 |       1 |
| Red Rock Canyon Visitor Center                 | Las Vegas | Travel Services               |   4.5 |           32 |       1 |
| Big Wong Restaurant                            | Las Vegas | Taiwanese                     |   4.0 |          768 |       1 |
| Sweet Ruby Jane Confections                    | Las Vegas | Specialty Food                |   4.0 |           30 |       0 |
| Red Rock Canyon Visitor Center                 | Las Vegas | Special Education             |   4.5 |           32 |       1 |
| Big Wong Restaurant                            | Las Vegas | Soup                          |   4.0 |          768 |       1 |
| Motors & More                                  | Las Vegas | Solar Installation            |   5.0 |            7 |       1 |
| Wooly Wonders                                  | Las Vegas | Shopping                      |   3.5 |           11 |       0 |
| Red Rock Canyon Visitor Center                 | Las Vegas | Shopping                      |   4.5 |           32 |       1 |
| Walgreens                                      | Las Vegas | Shopping                      |   2.5 |            6 |       1 |
| Desert Medical Equipment                       | Las Vegas | Shopping                      |   5.0 |            4 |       1 |
| Jacques Cafe                                   | Las Vegas | Sandwiches                    |   4.0 |          168 |       0 |
| Jacques Cafe                                   | Las Vegas | Restaurants                   |   4.0 |          168 |       0 |
| Wingstop                                       | Las Vegas | Restaurants                   |   3.0 |          123 |       1 |
| Big Wong Restaurant                            | Las Vegas | Restaurants                   |   4.0 |          768 |       1 |
| Hibachi-San                                    | Las Vegas | Restaurants                   |   4.5 |            3 |       0 |
| WorldMark Las Vegas - Spencer Street           | Las Vegas | Resorts                       |   3.5 |           19 |       1 |
| Vue at Centennial                              | Las Vegas | Real Estate                   |   4.0 |            6 |       1 |
| Red Rock Canyon Visitor Center                 | Las Vegas | Professional Services         |   4.5 |           32 |       1 |
| Jon Petrick, DC - Las Vegas Pain Relief Center | Las Vegas | Physical Therapy              |   5.0 |            5 |       1 |
| Walgreens                                      | Las Vegas | Photography Stores & Services |   2.5 |            6 |       1 |
| Anthem Pediatrics                              | Las Vegas | Pediatricians                 |   4.0 |           16 |       1 |
| Children's Dental Center                       | Las Vegas | Pediatric Dentists            |   4.0 |           11 |       1 |
+------------------------------------------------+-----------+-------------------------------+-------+--------------+---------+
(Output limit exceeded, 25 of 78 total rows shown)
```

Query 2:
```
Select category, COUNT(*) AS NoOfBusiness,avg(stars) As StarReviews, Avg(review_count) AS Avgreviews FROm
business LEFT JOIN category
on business.id = category.business_id
LEFT JOIN hours
on business.id = hours.business_id
WHERE business.is_open =1
GROUP BY category
HAVING NoOfBusiness >10
ORDER BY StarReviews DESC
```
Result:
```
+-----------------------+--------------+---------------+---------------+
| category              | NoOfBusiness |   StarReviews |    Avgreviews |
+-----------------------+--------------+---------------+---------------+
| Fashion               |           14 | 4.71428571429 | 6.78571428571 |
| Education             |           12 | 4.70833333333 |         20.75 |
| Hiking                |           15 | 4.66666666667 |          19.6 |
| Auto Repair           |           18 | 4.63888888889 |          28.0 |
| Carpet Cleaning       |           12 |           4.5 | 7.58333333333 |
| Oil Change Stations   |           11 | 4.45454545455 | 40.6363636364 |
| Local Services        |           58 | 4.43103448276 | 9.55172413793 |
| Active Life           |           43 | 4.38372093023 | 13.6744186047 |
| Automotive            |           39 | 4.37179487179 | 22.4358974359 |
| Health & Medical      |           70 | 4.28571428571 | 12.9142857143 |
| Professional Services |           25 |          4.26 |          77.8 |
| Apartments            |           16 |          4.25 |          5.75 |
| Flowers & Gifts       |           14 |          4.25 |          18.5 |
| Gift Shops            |           14 |          4.25 |          18.5 |
| Japanese              |           14 |          4.25 |          35.5 |
| Real Estate           |           16 |          4.25 |          5.75 |
| Travel Services       |           19 | 4.23684210526 |         115.0 |
| Home Services         |           64 |      4.234375 |       6.65625 |
| Home Cleaning         |           13 | 4.23076923077 | 7.38461538462 |
| Fitness & Instruction |           18 | 4.22222222222 | 11.9444444444 |
| Home & Garden         |           20 |           4.2 |           6.0 |
| Bakeries              |           25 |          4.18 |         51.64 |
| Art Galleries         |           13 | 4.15384615385 | 16.9230769231 |
| Specialty Food        |           13 | 4.15384615385 | 304.692307692 |
| Sandwiches            |           28 | 4.08928571429 | 164.321428571 |
+-----------------------+--------------+---------------+---------------+
(Output limit exceeded, 25 of 59 total rows shown)  
```
Query 3: 
```
SELECT  C.Category
        , AVG(B.review_count) AS Avg_Number_Of_Reviews
        , AVG(b.stars)
FROM category c INNER JOIN business b ON b.id = c.business_id
WHERE C.Category IN ("Chinese","French","Indian","Italian","Japanese","Korean","Mexican")
GROUP BY c.category 
ORDER BY AVG(b.stars) DESC
```
Result:
```
+----------+-----------------------+--------------+
| category | Avg_Number_Of_Reviews | AVG(b.stars) |
+----------+-----------------------+--------------+
| Korean   |                  31.5 |         4.25 |
| French   |                 128.5 |          4.0 |
| Japanese |                  30.4 |          3.8 |
| Indian   |                  12.6 |          3.6 |
| Italian  |                  74.0 |          3.5 |
| Mexican  |         46.7142857143 |          3.5 |
| Chinese  |                 199.0 |        3.125 |
+----------+-----------------------+--------------+     
```        
?? 2022 GitHub, Inc.
Terms
Privacy
Security
Status
Docs
Contact GitHub
Pricing
API
Training
Blog
About
