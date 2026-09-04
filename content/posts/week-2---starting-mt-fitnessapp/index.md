+++

date = '2026-09-04T13:35:33+02:00'

draft = false

title = 'Week 2 – Starting My Fitness website'

+++



\# What I have been working on



This week, I started working on my portfolio website while also continuing development on my Fitness Tracker project.



The goal of the Fitness Tracker is to allow users to keep track of their daily calorie and nutritional intake. I have been working on both the backend structure and the database that will support the application.



\## JPA and Database



I have been working with \*\*Java, JPA, Hibernate, and PostgreSQL\*\* to design the database structure for the application.



I created several entities and relationships, including:



\* `User`

\* `UserDetails`

\* `DailyLog`

\* `Meal`

\* `Food`

\* `FoodAmount`



The database is structured using primary keys and foreign keys to connect the different entities. For example, a user can have multiple daily logs, a daily log can contain multiple meals, and each meal can contain multiple food items.



I have also been working with different JPA relationships such as:



\* `@OneToOne`

\* `@OneToMany`

\* `@ManyToOne`



I have used bidirectional relationships in my entities and worked with methods for keeping both sides of the relationships updated.



\## REST API and Food Data



Another part of the project is working with APIs to retrieve food and nutritional information.



The idea is that users will be able to search for food or use a barcode to find a product and retrieve information such as:



\* Calories

\* Protein

\* Carbohydrates

\* Fat

\* Sugar

\* Fibre

\* Salt

\* Saturated fat



The retrieved food information can then be stored in the database and connected to the user's meals through the `FoodAmount` entity.



\## Portfolio Website



Alongside the programming project, I have started building my portfolio using \*\*Hugo\*\* and the \*\*Blowfish theme\*\*.



The purpose of the portfolio is to document my development as a Datamatiker student and showcase the projects and technologies I work with.



I have learned how to:



\* Create and structure a Hugo website

\* Use the Blowfish theme

\* Create posts and articles

\* Write content using Markdown

\* Organize content on the website

\* Document my programming projects and development process



This is the first week of my portfolio, and I will continue documenting my progress as I develop the Fitness Tracker and work with new technologies such as Java, JPA, databases, REST APIs, and web development.



