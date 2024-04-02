# Calculating-Free-to-Paid-Conversion-Rate


Import the db_course_conversions database—stored in the db_course_conversions.sql file—into your schemas and study its content. Then, by appropriately joining and aggregating the tables, create a new result dataset comprising the following columns:

student_id – (int) the unique identification of a student

date_registered – (date) the date on which the student registered on the 365 platform

first_date_watched – (date) the date of the first engagement

first_date_purchased – (date) the date of first-time purchase (NULL if they have no purchases)

date_diff_reg_watch – (int) the difference in days between the registration date and the date of first-time engagement

date_diff_watch_purch – (int) the difference in days between the date of first-time engagement and the date of first-time purchase (NULL if they have no purchases)
Hint: Research the DATEDIFF function in MySQL.



The resulting set you retrieve should include the student IDs of students entering the diagram’s shaded region. Additionally, your objective is to determine the conversion rate of students who have already watched a lecture. Therefore, filter your result dataset so that the date of first-time engagement comes before (or is equal to) the date of first-time purchase.

Sanity check: The number of records in the resulting set should be 20,255.

To complete the task, follow the instructions below.

First, remember to import the db_course_conversions database and refresh the Schemas pane to see it appear. Apply the USE keyword to use the named database as the default (current) one.
Retrieve the columns one by one as listed in the task. Use the MIN aggregate function to find the first-time engagement and purchase dates. Apply the DATEDIFF function to see the difference in the respective days. 
SELECT 

    ???,
    
    ???,
    
    MIN(???) AS first_date_watched,
    
    MIN(???) AS first_date_purchased,
    
    DATEDIFF(???) AS days_diff_reg_watch,
    
    DATEDIFF(???) AS days_diff_watch_purch
    

FROM

    student_engagement e
    
        ???
        
    student_info i ON ???
    
        ???
        
    student_purchases p ON ???
    
Applying the MIN aggregate function in the previous step requires grouping the results appropriately.

SELECT 

    ???,
    
    ???,
    
    MIN(???) AS first_date_watched,
    
    MIN(???) AS first_date_purchased,
    
    DATEDIFF(???) AS days_diff_reg_watch,
    
    DATEDIFF(???) AS days_diff_watch_purch
    
FROM

    student_engagement e
    
        ???
        
    student_info i ON ???

    
    student_purchases p ON ???
    
GROUP BY ???;

Filter the data to exclude the records where the date of first-time engagement comes later than the date of first-time purchase. Remember to keep the students who have never made a purchase.

SELECT 

    ???,
    
    ???,
    
    MIN(???) AS first_date_watched,
    
    MIN(???) AS first_date_purchased,
    
    DATEDIFF(???) AS days_diff_reg_watch,
    
    DATEDIFF(???) AS days_diff_watch_purch
    
FROM

    student_engagement e
    
        ???
        
    student_info i ON ???
    
        ???
        
    student_purchases p ON ???
    
GROUP BY ???

HAVING ???;






Free-to-Paid Conversion Rate:
This metric measures the proportion of engaged students who choose to benefit from full course access on the 365 platform by purchasing a subscription after watching a lecture. It is calculated as the ratio between:

The number of students who watched a lecture and purchased a subscription on the same day or later.
The total number of students who have watched a lecture.
Convert the result to percentages and call the field conversion_rate.

Average Duration Between Registration and First-Time Engagement:
This metric measures the average duration between the date of registration and the date of first-time engagement. This will tell us how long it takes, on average, for a student to watch a lecture after registration. The metric is calculated by finding the ratio between:

The sum of all such durations.
The count of these durations, or alternatively, the number of students who have watched a lecture.
Call the field av_reg_watch.

Average Duration Between First-Time Engagement and First-Time Purchase:
This metric measures the average time it takes individuals to subscribe to the platform after viewing a lecture. It is calculated by dividing:

The sum of all such durations.
The count of these durations, or alternatively, the number of students who have made a purchase.
Call the field av_watch_purch.

Use the following instructions to carry out the task.

Surround the subquery you created in the previous part (Create the Subquery) in parentheses and give it an alias, say a.
Consider the skeleton below. Fill in the appropriate columns to retrieve the three metrics described in this task. The results are rounded to two decimal places for clarity. Don’t forget to convert the conversion_rate metric to percentages.

SELECT 

    ROUND(COUNT(???) / COUNT(???),
    
            2) AS conversion_rate,
            
    ROUND(SUM(???) / COUNT(???),
    
            2) AS av_reg_watch,
            
    ROUND(SUM(???) / COUNT(???),
    
            2) AS av_watch_purch
            
FROM

    (
    
        -- Subquery
        
    ) a;
