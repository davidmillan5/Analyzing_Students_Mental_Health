# Analyzing Student's Mental Health

## Project Description

Studying abroad can be both exciting and difficult. But what might be contributing to this? One Japanese international university decided to find out!

Use your data manipulation skills to explore the data from a study on the mental health of international students, and find out which factors may have the greatest impact.

## Tools

In this project I will use SQL to response relevant questions around the dataset that will give you an important insight into the mental health state of international students abroad.

- Used relational database
  - [PostgreSQL](https://www.postgresql.org/)


## Summary

Explore and analyze the **students** data to see how the length of stay (**stay**) impacts the average mental health diagnostic scores of the international students present in the study.

- Return a table with nine rows and five columns.
- The five columns should be aliased as: stay, count_int,         average_phq, average_scs, and average_as, in that order.
- The average columns should contain the average of the todep (PHQ-9 test), tosc (SCS test), and toas (ASISS test) columns for each length of stay, rounded to two decimal places.
- The count_int column should be the number of international students for each length of stay.
- Sort the results by the length of stay in descending order.

![Descriptive Alt Text](https://img-cdn.inc.com/image/upload/f_webp,c_fit,w_828,q_auto/vip/2025/07/GettyImages-1361377657.jpg)


Does going to university in a different country affect your mental health? A Japanese international university surveyed its students in 2018 and published a study the following year that was approved by several ethical and regulatory boards.

The study found that international students have a higher risk of mental health difficulties than the general population, and that social connectedness (belonging to a social group) and acculturative stress (stress associated with joining a new culture) are predictive of depression.

Explore the students data using PostgreSQL to find out if you would come to a similar conclusion for international students and see if the length of stay is a contributing factor.

Here is a data description of the columns you may find helpful.

| Field Name     | Description                                                  |
|----------------|--------------------------------------------------------------|
| inter_dom      | Types of students (international or domestic)               |
| japanese_cate  | Japanese language proficiency                               |
| english_cate   | English language proficiency                                |
| academic       | Current academic level (undergraduate or graduate)          |
| age            | Current age of student                                      |
| stay           | Current length of stay in years                              |
| todep          | Total score of depression (PHQ-9 test)                       |
| tosc           | Total score of social connectedness (SCS test)               |
| toas           | Total score of acculturative stress (ASISS test)             |


## Walkhrough

1. Verfy the CSV source file structure and identify the amount of columns in it that we will use and find if theey already have a header, that we will use as our columns name.
2. Open pgAdmin an create a new database that for this case we will call **students_db**.
3. Create the table inside the database using the **Query tool** and execute the following query:


```sql
CREATE TABLE students (
    inter_dom TEXT,
    region TEXT,
    gender TEXT,
    academic TEXT,
    age INTEGER,
    age_cate TEXT,
    stay INTEGER,
    stay_cate TEXT,

    japanese INTEGER,
    japanese_cate TEXT,
    english INTEGER,
    english_cate TEXT,

    intimate TEXT,
    religion TEXT,
    suicide TEXT,
    dep TEXT,
    deptype TEXT,
    todep INTEGER,
    depsev TEXT,

    tosc INTEGER,
    apd INTEGER,
    ahome INTEGER,
    aph INTEGER,
    afear INTEGER,
    acs INTEGER,
    aguilt INTEGER,
    amiscell INTEGER,
    toas INTEGER,

    partner TEXT,
    friends TEXT,
    parents TEXT,
    relative TEXT,
    profess TEXT,
    phone TEXT,
    doctor TEXT,
    reli TEXT,
    alone TEXT,
    others TEXT,
    internet TEXT,

    partner_bi TEXT,
    friends_bi TEXT,
    parents_bi TEXT,
    relative_bi TEXT,
    professional_bi TEXT,
    phone_bi TEXT,
    doctor_bi TEXT,
    religion_bi TEXT,
    alone_bi TEXT,
    others_bi TEXT,
    internet_bi TEXT
);

```

4. Import the data in the csv into pgAdmin to create the whole table in the database.


5. Solution Query

```sql
SELECT
	stay AS stay,
	ROUND(COUNT(inter_dom),2) AS count_int,
	ROUND(AVG(todep),2) AS average_phq,
	ROUND(AVG(tosc),2) AS average_scs,
	ROUND(AVG(toas),2) AS average_as
FROM
	students
WHERE 
	inter_dom = 'Inter'
GROUP BY
	stay
ORDER BY
	stay DESC
LIMIT
	9;

```


### Results

| stay | count_int | average_phq | average_scs | average_as |
|------|-----------|-------------|-------------|------------|
| 10   | 1.00      | 13.00       | 32.00       | 50.00      |
| 8    | 1.00      | 10.00       | 44.00       | 65.00      |
| 7    | 1.00      | 4.00        | 48.00       | 45.00      |
| 6    | 3.00      | 6.00        | 38.00       | 58.67      |
| 5    | 1.00      | 0.00        | 34.00       | 91.00      |
| 4    | 14.00     | 8.57        | 33.93       | 87.71      |
| 3    | 46.00     | 9.09        | 37.13       | 78.00      |
| 2    | 39.00     | 8.28        | 37.08       | 77.67      |
| 1    | 95.00     | 7.48        | 38.11       | 72.80      |


### Conclusions

Based on the the query that we made to extract the information... Explore and analyze the students data to see how the length of stay (stay) impacts the average mental health diagnostic scores of the international students present in the study.