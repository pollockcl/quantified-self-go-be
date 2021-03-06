# README

An (in progress) backend for quantified-self-fe written in Go.

## Setup
>You must have PostGreSQL installed and running!!!

>Create the database OR change the db.go to point to a database of your choice

```
   psql postgres
   CREATE DATABASE qs_go
```

>Create tables

```
   psql qs_go
   CREATE TABLE foods (id SERIAL PRIMARY KEY, name VARCHAR(255) NOT NULL, calories INT NOT NULL)
   CREATE TABLE meals (id SERIAL PRIMARY KEY, name VARCHAR(255) NOT NULL)
   CREATE TABLE meal_foods (id SERIAL PRIMARY KEY, food_id NOT NULL, meal_id NOT NULL)
```

>Export environment variables in the terminal

```
   export USER=username
   export PASSWORD=password
   export DBNAME=dbname
   export SSLMODE=disable
   export HOST=localhost
```

>Clone this Repo

```git clone https://github.com/pollockcl/quantified-self-go-be```


>Compile the app


```go build```


>Run the executable


```./api```

# Endpoints
## GET /api/v1/foods
>Returns all foods currently in the database

## GET /api/v1/foods/:id
>Returns the food object with the specific :id passed in or 404 if the food is not found

## POST /api/v1/foods

>Allows creating a new food with the parameters:

```{ "food": { "name": "Name of food here", "calories": "Calories here"} }```

>If food is successfully created, the food item will be returned. If the food is not successfully created, a 400 status code will be returned. Both name and calories are required fields.

## PATCH /api/v1/foods/:id

>Allows one to update an existing food with the parameters:

```{ "food": { "name": "Mint", "calories": "14"} }```
>If food is successfully updated (name and calories are required fields), the food item will be returned. If the food is not successfully updated, a 400 status code will be returned.

## DELETE /api/v1/foods/:id

>Will delete the food with the id passed in and return a 204 status code. If the food can’t be found, a 404 will be returned.

## GET /api/v1/meals

>Returns all the meals in the database along with their associated foods

## GET /api/v1/meals/:meal_id/foods

>Returns all the foods associated with the meal with an id specified by :meal_id or a 404 if the meal is not found

## POST /api/v1/meals/:meal_id/foods/:id

>Adds the food with :id to the meal with :meal_id

>This creates a new record in the MealFoods table to establish the relationship between this food and meal. If the meal/food cannot be found, a 404 will be returned.
>If successful, this request will return a status code of 201 with the following body:
```{ "message": "Successfully added FOODNAME to MEALNAME" }```

## DELETE /api/v1/meals/:meal_id/foods/:id

>Removes the food with :id from the meal with :meal_id

>This deletes the existing record in the MealFoods table that creates the relationship between this food and meal. If the meal/food cannot be found, a 404 will be returned.

>If successful, this request will return:

```{ "message": "Successfully removed FOODNAME to MEALNAME" }```

