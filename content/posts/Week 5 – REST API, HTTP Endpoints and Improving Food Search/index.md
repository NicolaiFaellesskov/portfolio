+++
date = '2026-10-02T13:00:00+02:00'
draft = false
title = 'Week 5 – REST API, HTTP Endpoints and Improving Food Search'
+++

What I have been working on

This week, I continued working on my Fitness Tracker project, focusing on REST API endpoints, DailyLogs, and improving the food search.

REST API and Javalin

I worked more with REST APIs and HTTP requests in the Fitness Tracker.

I created and tested different REST API endpoints using GET, POST, PUT, and DELETE. This allowed me to create, read, update, and delete data through HTTP requests.

DailyLog

I worked with the DailyLog functionality and tested the CRUD operations through the REST API.

The application can now retrieve all DailyLogs, retrieve a DailyLog by ID, create a new DailyLog, update an existing DailyLog, and delete a DailyLog.

I also created HTTP requests to test these endpoints and make sure that the REST API works as expected.

Improving Food Search

I continued improving the food search using the Open Food Facts API.

I tested the search with different queries and found that searches with multiple words were not always handled correctly by the scoring system.

For example, `Chicken_Breast` was treated as one word instead of two separate words. I changed the search handling so that `_` is treated as a space. This means that `Chicken_Breast` is now treated as `Chicken Breast`, which gives more relevant search results.

I also added tests for the food search to check how the search performs with different queries.

What I learned

This week I learned more about how REST APIs use HTTP methods such as GET, POST, PUT, and DELETE to work with resources in a web application.

I also got more experience with Javalin, HTTP requests, and testing REST API endpoints.

I learned more about how a search scoring system works and how normalizing the search input can improve the results from an external API.

Overall, the Fitness Tracker is becoming more functional, with more of the application being accessible through a REST API and the food search giving more relevant results.
+++
