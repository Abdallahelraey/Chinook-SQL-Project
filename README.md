# Chinook SQL Project

## Overview

This project involves analyzing a music database using SQL queries to gain insights into customer purchasing behavior, popular artists, and genre trends. The database is based on the Chinook database, which represents a digital media store.

## SQL Queries and Insights

### Query 1: Countries with the Most Rock Song Purchases

```sql
SELECT billingcountry,
       Count(*) AS rock_song
FROM   genre a
       JOIN track b
         ON a.genreid = b.genreid
            AND a.NAME = 'Rock'
       JOIN invoiceline c
         ON c.trackid = b.trackid
       JOIN invoice d
         ON c.invoiceid = d.invoiceid
GROUP  BY 1
ORDER  BY 2 DESC 
```

**Insight:** The USA has the highest number of rock song purchases.

### Query 2: Artists with the Most Rock Songs

```sql
SELECT d.Name,
       count(b.Name) AS songs
FROM Genre a
JOIN Track b ON b.GenreId = a.GenreId
AND a.Name = 'Rock'
JOIN Album c ON c.AlbumId = b.AlbumId
JOIN Artist d ON d.ArtistId = c.ArtistId
GROUP BY 1
ORDER BY 2 DESC
```

**Insight:** LED ZEPPELIN and U2 are among the top artists with the most rock songs.

### Query 3: Top Earning Artists

```sql
SELECT a.Name AS Artist,
       sum(c.UnitPrice * Quantity) AS Total_earnings_by_user
FROM Artist a
JOIN Album b ON a.ArtistId = b.ArtistId
JOIN Track c ON c.AlbumId = b.AlbumId
JOIN InvoiceLine d ON d.TrackId = c.TrackId
JOIN Invoice e ON e.InvoiceId = d.InvoiceId
GROUP BY 1
ORDER BY 2 DESC
LIMIT 10
```

**Insight:** IRON MAIDEN is the artist who has earned the most according to the Invoice Lines.

### Query 4: Most Popular Music Genres

```sql
SELECT a.name,
       count(*) AS num_tracks
FROM Genre a
JOIN Track b ON a.GenreId = b.GenreId
GROUP BY 1
ORDER BY 2 DESC
```

**Insight:** Rock music is the most popular genre in the store.

## Visual Insights

Based on the queries, the following insights were visualized:

- **Countries that purchase the most rock songs:** The USA leads, followed by Canada and Brazil.
- **Top 10 bands with the most rock songs:** LED ZEPPELIN, U2, and DEEP PURPLE are among the top.
- **Top earning artists:** IRON MAIDEN, U2, and METALLICA are the highest earners.
- **Trending music genres:** Rock, Latin, and Metal are the top genres.

## Requirements

To run these queries, you need access to an SQL database client and the Chinook database.

## Project Structure

```plaintext
.
├── README.md
└── chinook_queries.sql
```

- `README.md`: This file.
- `chinook_queries.sql`: Contains the SQL queries used for the analysis.

## Acknowledgements

This project is based on the Chinook database and was created as part of an SQL learning exercise.

