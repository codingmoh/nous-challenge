# NOUS Coding challenge

## Introduction
Our SaaS-Solution aims to automate the way cleaning processes are organized. 
We build service oriented REST APIs, which allow customers to create cleaning plans.

As you continue reading the requirements of this assessment, we like to point out that we expect you to treat it like a real world task. You shall design your API, code, commits, tests, comments and database like you'd be doing in your job.

## Requirements
Your task is to build a REST API, that allows the creation of a cleaning plans and subsequently the manipulation of those. 

This repository provides a project that is already preconfigured and contains a setup that can be used. 
You are expected to use asp.net core 5.0, entityframework core 5.0 and therefore store your data in a database. (e.g.: sqlite, in-memory)

### asp.net core controller
You have to figure out which http methods to use, how to configure the routes and how to store the data. There's an empty controller in the project you can use to add your endpoints. You can find it in `CleaningManagementApi\CleaningManagement.Api\Controller\CleaningManagementController.cs`

### Database, DbContext, ef core
You can reuse the DbContext in `CleaningManagement.DAL\CleaningManagementDbContext.cs` that uses an in memory database, but you're allowed to use a different setup if prefered

---
## Cleaning Plan Model
A cleaning plan consists of following attributes:
* A __required__ Title with a max. length of 256 characters. 
* A __required__ customer identification number (=`CustomerId`)
* An __autogenerated__ creation date, that identifies the datetime of the created plan.
* An __optional__ description with a max. length of 512 characters.

An endpoint must always validate the provided data and respond with adequate http status codes in case of success or error.

---
# Cleaning Plan Endpoints

## Endpoint: Create Cleaning Plan
This endpoint should allow clients to create a cleaning plan. Using the constraints 

Example **request** body:
```
{ 
   "title": "Hotel Room Cleaning, double bed",
   "customerId": 123223,
   "description": "This plan is meant to be used for double bed rooms."
}
```

If cleaning plans are successfully created, An expected response should contain the provided data, the Id and the creation date.


Example response body:
```
{
   "id": "8c442581-c67a-41e5-8d2d-b1176de31087"
   "title": "Hotel Room Cleaning, double bed",
   "customerId": 123223,
   "description": "This plan is meant to be used for double bed rooms.",
   "createdAt" : "2022-01-01T23:00:00Z"
}
```

## Endpoint: List Cleaning Plans
This endpoint should provide a list of all cleaningplans using a provided `customerId`. 
An empty response body should be provided, if a `customerId` is being used, that does not exist.

Example response body:
```
[
  {
    "id": "8c442581-c67a-41e5-8d2d-b1176de31087"
    "title": "Hotel Room Cleaning, double bed",
    "customerId": 123223,
    "description": "This plan is meant to be used for double bed rooms.",
    "createdAt" : "2022-01-01T23:00:00Z"
  },
  {
    "id": "8c442581-c67a-41e5-8d2d-b1176de31087"
    "title": "Mall Cleaning, inner city",
    "customerId": 123223,
    "description": "Suitable only for malls smaller than 23000 m².",
    "createdAt" : "2022-01-02T23:12:22Z"
  }, 
  ...
]
```

## Endpoint: Update Cleaning Plan information using its id
This endpoint should allow a client to update a cleaning plan using its id. A client should be able to update the cleaning plan fields. 

Example **request** body:
```
{ 
   "title": "Hotel Room Cleaning, double bed",
   "customerId": 123223,
   "description": "This plan is meant to be used for double bed rooms."
}
```

## Endpoint: Delete Cleaning Plan by id
This endpoint should allow a client to delete a cleaning plan using its id.

Example response body:
```
[
  {
    "id": "8c442581-c67a-41e5-8d2d-b1176de31087"
    "title": "Hotel Room Cleaning, double bed",
    "customerId": 123223,
    "description": "This plan is meant to be used for double bed rooms.",
    "createdAt" : "2022-01-01T23:00:00Z"
  },
  {
    "id": "8c442581-c67a-41e5-8d2d-b1176de31087"
    "title": "Mall Cleaning, inner city",
    "customerId": 123223,
    "description": "Suitable only for malls smaller than 23000 m².",
    "createdAt" : "2022-01-02T23:12:22Z"
  }, 
  ...
]
```

## Summary
In summary you shall design and write a REST API, which has at least following endpoints:
* Endpoint for creating a cleaning plan for a certain customer
* Endpoint that lists all cleaning plans of a certain customer
* Endpoint that provides a single cleaning plan by its cleaning plan id.
* Endpoint that deletes a cleaning plan using its id