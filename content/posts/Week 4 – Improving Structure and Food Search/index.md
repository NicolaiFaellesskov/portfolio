+++

date = '2026-09-25T13:00:00+02:00'

draft = false

title = 'Week 4 – Improving Structure and Food Search'

+++

# What I have been working on

This week, I continued working on my Fitness Tracker project, focusing on improving the structure of the application, working more with the database layer, and improving the food search.

## DAO and Mappers

I added DAOs for the entities in the application so that database-related operations are separated from the rest of the application.

I also added mappers to handle the conversion between entities and DTOs. This has made the code easier to structure and keeps the different responsibilities more separated.

## Food Search

I continued working on the food search using the Open Food Facts API.

I created a test for the food search to make sure that the search returns the expected result.

I also worked on improving the speed of the search. I adjusted the number of threads used by the asynchronous food search, which helped make the search more efficient without creating unnecessary concurrent requests.

## Javalin and Food Data

I added Javalin to the Fitness Tracker so that food data can be accessed through an endpoint.

This means that I can now see information about a food and its nutrients through the application. This is also the first step towards having a small frontend/API interface for the Fitness Tracker.

## Improving the Code Structure

I spent some time cleaning up the code and improving the overall structure of the project.

I separated responsibilities between the different parts of the application, making the code easier to understand and maintain.

## What I learned

This week I learned more about how DAOs and mappers can be used to structure a Java application.

I also got more experience with testing, asynchronous tasks, Javalin, and working with data from an external API.

Overall, the project is becoming more structured, and the different parts of the application are starting to work together more clearly.
+++
