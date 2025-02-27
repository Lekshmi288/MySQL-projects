# SQL Analysis of the Chinook Music Store Dataset

In this project, I perform basic and advanced analysis of the Chinook database using SQL queries and functions.

Learning objectives:
* setup a docker container with mysql server
* write basic SQL queries for data retrieval
* perform complex joins across multiple tables
* group and aggregate data using SQL functions
* utilize window functions for advanced analysis

## Section 1: Basic SQL commands (14 questions)

You are a data analyst in the Chinook company who has just been asked to conduct a full analysis of sales data of the artist named "Queen" in your database. The company needs to understand how well a specific artist is performing by reviewing the tracks sold, the total revenue generated, and customer information related to purchases. Your final goal is to present a summary of sales and customer details for that artist.

**Requirement:** Use subquery to answer the questions in section 1. We'll have an entire section dedicated to joins.

### Part 1: Analysis of the artist "Queen"

We would recommend you to explore all the tables by using appropriate SQL queries to display the corresponding table rows. Also, to make your notebook readable, we recommend copy/pasting the questions into mark down cells above your solution cell. You can use `####` mark down syntax to highlight each question.

**Requirement**: Each solution cell should be marked using the appropriate question number as a comment. For example, at the beginning of the cell answering question 1, you should have this comment: "#q1".

#### Q1: Retrieve all information about the artist "Queen" from the Artist table.

#### Q2: What are all the albums released by the artist "Queen"?

#### Q3: What are all the tracks released by the artist "Queen"? 

#### Q4: How many tracks released by "Queen" were composed or co-composed by "Queen"?

**Requirement:** Your result should have count column named as `TotalQueenTracks`

#### Q5: Who are all the composers of tracks by the artist "Queen"?

**Requirement:** Your result should only include unique composer names.

#### Q6: Which are the top 5 longest tracks by the artist "Queen"?

#### Q7: What are all the tracks by the artist "Queen" that are sized smaller than 6MB?

#### Q8: Generate human-readable details about all tracks released by "Queen".

**Requirement:** Other than track names, your result should have two columns named `DurationMinutes` and `FileSize` in MB.

### Part 2: Customer and employee analysis

Let's now explore the customers to see if there is some trend.

#### Q9: Who are all the customers from USA?

**Requirement:** Your result should include `CustomerId`, `FirstName`, `LastName`, and `State` information for the customers. The rows should be ordered using ascending order of the `State` names.

#### Q10: Which invoices correspond to transactions costing greater than $20?

#### Q11: Which invoices were issued in the year 2021?

#### Q12: What was the total expenditure of "Eduardo Martins"?

#### Q13: Which customers from the USA do not have any specified company information?

#### Q14: Who are all the Canadian employess?

## Section 2: In-depth analysis of Queen data with `JOIN` clauses (10 questions)

Now that you have the basic information and understanding of the database, you should begin some real analysis that can uncover interesting information across tables. In SQL, we link tables using the `JOIN` command.

#### Q15: Retrieve the names of all customers along with their corresponding invoice totals.

**Requirements:** 
* You must use `JOIN` to solve this question and the other questions in this section.
* Your results should be ordered by `LastName` (A through Z).
* Your results should also be ordered based on increasing order of the `Total` column.

#### Q16: Which customers purchased the tracks by "Queen"?

**Requirements:** 
* Your result should include `CustomerId`, `FirstName`, and `LastName` of customers who have purchased tracks by Queen.
* Your results should only include unique `CustomerID`.
* Your results should be ordered by `CustomerID`.
* You may use subquery for the Queen's tracks retrieval part given that you wrote that for Q3, but you must use `JOIN` for answering the rest of the question.

#### Q17: Retrieve Invoice Details for the tracks by "Queen".

**Requirements:** 
* Your results must include the `InvoiceId`, `InvoiceDate`, `BillingCountry`, and `Total` columns for invoices that include at least one track by Queen.
* Your results should only include unique `InvoiceId`.
* Your results should be ordered by `InvoiceId`.

#### Q18: Retrieve tracks details by "Queen" along with the corresponding album titles and media types.

**Requirements:** 
* Your results must include `TrackId`, track's name `TrackName`, album's title `AlbumTitle`, and media type's name `MediaTypeName` for all tracks by Queen.
* Your results should be ordered by `TrackId`.

#### Q19: Find genres of tracks by "Queen".

**Requirements:** 
* Your results must include `TrackId`, track's name `TrackName`, and genre's name `GenreName` for all tracks by Queen.
* Your results should be ordered by `TrackId`.

#### Q20: Retrieve invoice details for customers from the USA who purchased tracks by "Queen".

**Requirements:** 
* Your results must include the `InvoiceId`, `InvoiceDate`, `BillingCity`, `BillingState`, and `CustomerId` for the invoices of customers from the USA who have purchased tracks by Queen.
* Your results should only include unique `InvoiceId`.
* Your results should be ordered by `InvoiceId`.

#### Q21: Find all playlists that contain tracks by "Queen".

**Requirements:** 
* Your results must include the playlist name `PlaylistName`.
* Your results should also be ordered based on ascending order of `PlaylistName`.

#### Q22: List all the employees (sales agents) who supported customers that purchased tracks by "Queen." 

**Requirements:** 
* Your results must include the `EmployeeId`, `FirstName`, and `LastName`, of the employess (salees agents) who supported customers that purchased tracks by Queen.
* Your results should only include unique `EmployeeId`.
* Your results should be ordered by `EmployeeId`.

#### Q23: Retrieve a list of all albums along with the names of their artists, including albums that don't have any artist information.

**Requirements:** 
* **IMPORTANT NOTE:** You may **NOT** use a regular join to answer this question. Instead, you **MUST** use `LEFT JOIN`.
* Your result should include album title `AlbumTitle`, and artist name `ArtistName`.
* Your results should be ordered by ascending order of `AlbumTitle` and ascending order of `ArtistName`.
* Please run the below two queries **before** your solution query.

```python
conn.execute(text("""
    ALTER TABLE Album MODIFY Title VARCHAR(255) COLLATE utf8mb4_general_ci;
"""))

conn.execute(text("""
    SET collation_connection = 'utf8mb4_general_ci';
"""))
```

#### Q24: Retrieve a list of all artists and their corresponding albums, including artists who have not released any albums.

**Requirements:** 
* **IMPORTANT NOTE**: You may **NOT** use a regular join to answer this question. Instead, you **MUST** use `RIGHT JOIN`.
* Your result should include album title `AlbumTitle`, and artist name `ArtistName`.
* Your results should be ordered by ascending order of `AlbumTitle` and ascending order of `ArtistName`.

## Section 3: Grouping and windowing (11 questions)

In this section, you will employ SQL **grouping** clause and **windowing** functions to perform more complex data analysis. These queries will help you uncover the trends, summarize data, and obtain insights into the database. 

### Part 1: Basic grouping

#### Q25: How many tracks are there in each genre?

**Requirements:** 
* Your results must include the `GenreId`, and track count `TrackCount` for each genre.
* Your results should be ordered by descending order of track count.
* Your results should also be ordered by ascending order of `GenreId`.

#### Q26: What is the total duration (in hours) of tracks for top 5 longest albums?

**Requirements:** 
* Your results must include the `AlbumId`, album title `AlbumTitle` and total duration in hours `TotalDurationHours` for each album.
* Your results should be ordered by descending order of total duration in hours.

#### Q27: Retrieve all albums that contain tracks from more than one genre.

**Requirements:** 
* Your results must include the album title `AlbumTitle`, and corresponding unique genre count `GenreCount`.
* Your results should be ordered by descending order of genre count `GenreCount`.
* Your results should also be ordered by ascending order of `AlbumTitle`.

#### Q28: Calculate the total revenue for all artists.

**Requirements:** 
* Your results must include the artist name `ArtistName`, and corresponding total revenue `TotalRevenue`.
* Total revenue calculation: `UnitPrice * Quantity`
* Your results should be ordered by descending order of total revenue.
* Your results should also be ordered by ascending order of `ArtistName`.

#### Q29: Which genres have greater than 20 minute average track duration?

**Requirements:** 
* Your results must include the genre name `GenreName`, and corresponding average duration `AverageDurationMinutes` for tracks that have average duration that exceeds 20 minutes.
* Your results should be ordered by descending order of average duration in minutes.

#### Q30: What is the total expenditure incurred by customers who purchased tracks by "Queen"?

**Requirements:** 
* Your results must include the `CustomerId`, `FirstName`, `LastName`, and corresponding total expenditure `TotalExpenditure` then put the descending rank of total expenditure as `ExpenditureRank`.
* Total expenditure calculation: `UnitPrice * Quantity`
* Your results should be ordered by descending order of total expenditure.
* Your results should also be ordered by ascending order of `CustomerId`.

### Part 2: Windowing queries

Window functions allow you to perform calculations across a set of rows related to the current row, enabling advanced analysis without collapsing data.

#### Q31: Find each track's duration and rank all tracks by their duration.

**Requirements:** 
* Your results must include the `TrackId`, track name `TrackName`, duration in minutes `DurationMinutes`, and corresponding duration rank `DurationRank`.
* Ranking should be based on descending order of duration.
* Your results should be ordered by ascending order of ascending order of duration rank. If two tracks have the same rank, then they should be ordered based on descending order of duration in minutes.
* Your results should also be ordered by ascending order of `TrackId`.

#### Q32: Rank customers who purchased tracks by "Queen" based on their total expenditure.

**Hint:** You solved majority of this question already in Q30. Reuse that solution to answer this question

**Requirements:** 
* Your results must include the `CustomerId`, `FirstName`, `LastName`, corresponding total expenditure `TotalExpenditure`, and corresponding expenditure rank `ExpenditureRank`.
* Total expenditure calculation: `UnitPrice * Quantity`
* Ranking should be based on descending order of total expenditure.
* Your results should be ordered by descending order of total expenditure.
* Your results should also be ordered by ascending order of `CustomerId`.

### Q33: Calculate the total number of invoices for each customer and assign a sequential rank to each customer based on their total invoices.

**Requirements:**
* Your results must include the `CustomerId`, `FirstName`, `LastName`, corresponding invoices count `InvoicesCount`, and corresponding invoice rank `InvoiceRank`.
* Ranking:
  * Ranks assigned to customers must be unique and based on descending order of invoices count. That is customer with highest invoices count should receive rank 1.
  * If there are ties in invoices count, you must break ties by using ascending order of `LastName`. 

#### Q34: Find the top 3 invoices per country.

**Hints:** 
* This is a challenging question.
* Break it down into individual steps:
  1. Determine invoice rank `InvoiceRank` using descending order of `Total`. Make sure order the results both using ascending order of `BillingCountry` and `Total`.
  2. Then, write another query which uses the query you wrote in step 1 as sub query to filter invoices with top 3 ranks.

**Requirements:** 
* Your results must include the `BillingCountry`, `InvoiceId`, `Total`, and corresponding invoice rank `InvoiceRank`.
* Ranking should be based on descending order of `Total`.
* Your results should be ordered by the ascending order of `BillingCountry`, descending order of `Total`, and ascending order of `InvoiceId` in the exact sequence mentioned above. 

#### Q35: Calculate the moving average of monthly sales.

**Hints:** 
* This is a challenging question.
* Break it down into individual steps:
  1. Determine how to extract just the month information from `InvoiceDate` by exploring `DATE_FORMAT`.
  2. Then, calculate total sales per month and order the results by month.
  3. Finally, calculate moving average using `PRECEDING` and `CURRENT`.

**Requirements:** 
* Your results must include the month `Month`, corresponding month's total sales `MonthlySales`, and corresponding month's moving average sales `MovingAverageSales`.

