+++

date = '2026-09-11T13:00:00+02:00'

draft = false

title = 'Week 3 – Working with REST APIs and Asynchronous Tasks'

+++

# What I have been working on

This week, I continued working on my Fitness Tracker project, focusing mainly on REST APIs, JSON data, and asynchronous programming.

## REST APIs and JSON

I worked with external REST APIs to retrieve data from services such as Open Food Facts and TMDB.

I learned how to:

* Send HTTP GET requests using `HttpClient`
* Work with API URLs and parameters
* Receive JSON responses
* Convert JSON into Java DTOs using Jackson
* Use `JsonNode` to work with JSON data
* Use environment variables to store API keys securely

For the Fitness Tracker, I used the Open Food Facts API to search for food products and retrieve information such as calories, protein, carbohydrates, fat, sugar, fibre, salt, and saturated fat.

## Searching for Food

I improved the food search so that the application does not simply use the first product returned by the API.

Instead, I retrieve multiple results and use a simple scoring system to find the product that best matches the user's search.

The food data is then converted into a `FoodDTO` that can be used by the application.

## Asynchronous Programming

I also started working with asynchronous tasks and `Future`.

The food search now runs through a service that returns a `Future<FoodDTO>`. This taught me how a task can run separately from the main thread and how `future.get()` can be used to wait for the result.

This has helped me understand how asynchronous programming can be used when working with external APIs.

## What I learned

This week I learned more about how Java applications can communicate with external services and process the data they return.

I also gained a better understanding of JSON, DTOs, HTTP requests, API keys, and asynchronous programming with `Future`.

+++
