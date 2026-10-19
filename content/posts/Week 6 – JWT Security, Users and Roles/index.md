+++
date = '2026-10-19T09:00:00+02:00'
draft = false
title = 'Week 6 – JWT Security, Users and Roles'
+++

## What I have been working on

This week, I worked on the first part of the JWT Security assignment. The main focus was user management, password hashing, roles, and database operations using JPA and Hibernate.

## User and Role Entities

I created the `User` and `Role` entities to represent users and roles in the database.

The `User` entity contains information such as the username, password, and the roles assigned to the user. The `Role` entity represents roles that can be assigned to users, such as `USER` or `ADMIN`.

I also implemented a many-to-many relationship between users and roles. This allows a user to have multiple roles, while the same role can be assigned to multiple users.

## Password Hashing with BCrypt

I implemented password hashing using BCrypt.

When a user is created, the password is hashed before it is stored in the database. When a user logs in, the application verifies the entered password against the stored hash.

This is important because passwords should not be stored as plain text in the database.

## Security Interfaces and UserDAO

I implemented the `ISecurityUser` interface, which defines methods for verifying passwords and managing user roles.

I also worked with the `ISecurityDAO` interface and implemented its methods in `UserDAO`.

The DAO handles database operations such as creating users, verifying login credentials, creating roles, and assigning roles to users. I used JPA and Hibernate to perform these operations.

For database changes, I used transactions to make sure that changes are committed to the database.

## Database Configuration

While testing the application, I encountered a problem because PostgreSQL treats `USER` as a reserved keyword.

Hibernate was using the entity name `User` as the database table name, which caused an SQL syntax error. I fixed this by adding `@Table(name = "users")` to the `User` entity.

This allowed the Java entity to keep its original name while using `users` as the physical table name in the database.

## Testing

I created JUnit tests for the main `UserDAO` methods.

The tests check that users and roles can be created, that login credentials can be verified, and that roles can be assigned to users.

Testing helped me find the database table naming issue and verify that the DAO functionality works as expected after fixing it.

## What I learned

This week I learned more about how user management and security work in a Java application.

I gained experience with BCrypt password hashing, JPA relationships, database transactions, and the DAO pattern.

I also learned how Hibernate maps Java entities to database tables and how database naming can cause problems when using reserved keywords.

Overall, I have implemented and tested the main user and role functionality for the first part of the JWT Security assignment. This provides the foundation for handling authentication and authorization in the API.
+++