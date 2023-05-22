## Description

This project is a restaurant reservation system. It allows users to create, edit, cancel, and seat reservations. It also allows users to create, edit, and delete tables. The application is built with React, Bootstrap, Node, Express, Knex, PostgreSQL, and Jest.

## Website Link

Link: https://project-restaurant-reservation-fe.onrender.com
API Base Url: https://project-restaurant-reservation-dpnr.onrender.com

## Application Features

Any existing reservations and tables are displayed on the dashboard. Selecting the `next` button takes users to the next day, selecting `previous` takes users to the previous day, and `today` navigates users to the current day.
![Alt text](/Images/Screen%20Shot%202023-02-06%20at%202.19.38%20PM.png)

If there are no existing reservations on a specific day the reservations section will be left blank.
![Alt text](/Images/Screen%20Shot%202023-02-06%20at%202.24.58%20PM.png)

Selecting `New Reservation` allows you to create a new reservation. Users will be alerted of any errors they make when they are filling out the form.
![Alt text](/Images/Screen%20Shot%202023-02-06%20at%202.19.06%20PM.png)

When a form is submitted the dashboard for the reservation date previously submitted will be displayed. Users have the option of editing, canceling or seating a reservation.
![Alt text](/Images/Screen%20Shot%202023-02-06%20at%202.22.00%20PM.png)

Pressing the `Seat` button will navigate users to the seat form where employees can reserve a table for a reservation. Users will be alerted of any errors when they are filling out the form.
![Alt text](/Images/Screen%20Shot%202023-02-06%20at%202.24.18%20PM.png)

When a reservation is seated at a table, its status on the dashboard will be changed to `seated`. That table's status will display `occupied`.
![Alt text](/Images/Screen%20Shot%202023-02-07%20at%207.22.34%20PM.png)

Selecting the `Cancel` button will cause a pop up message to appear, which will give the user an option to cancel the reservation.
![Alt text](/Images/Screen%20Shot%202023-02-06%20at%202.25.37%20PM.png)

The `Edit` button navigates employees to the edit form, which allows them to edit reservations. Forms are prefilled with the current reservations data.
![Alt text](/Images/Screen%20Shot%202023-02-06%20at%202.20.51%20PM.png)

When a table is occupied, a `Finish` button will appear on the tables card. If the finish button is selected, a pop-up message will appear giving users the option to change the table's status back to `free`.
![Alt text](/Images/Screen%20Shot%202023-02-06%20at%202.24.45%20PM.png)

Selecting `New Table` allows users to create a new table
![Alt text](/Images/Screen%20Shot%202023-02-06%20at%202.20.13%20PM.png)

Selecting the `Search` button will take users to the search form where they can search for a reservation by their number.
![Alt text](/Images/Screen%20Shot%202023-02-06%20at%202.23.18%20PM.png)

## Technologies Used

`Back-end`

- Node
- Express
- Knex
- PostgreSQL (via ElephantSQL)
- Jest

`Front-end`

- React
- Bootstrap
- e2e tests
- Puppeteer

## Backend Endpoints
<details>
<summary>
Endpoint Description Summary
</summary>

- POST `/reservations` creates and returns a new reservation
- GET `/reservations?date='YYYY-MM-DD'` returns reservations by date (sorted asc)
- GET `/reservations?mobile_number=123` returns reservations by partial match of phone number
- GET `/reservations/:reservationId` returns reservation matching the reservationId
- PUT `/reservations/:reservationId` updates and returns the reservation matching the reservationId
- PUT `/reservations/:reservationId/status` updates only the status of a reservation
- GET `/tables` returns all Tables
- POST `/tables` creates and returns a new table
- PUT `/tables:table_id/seat` updates a table with a reservationId and changes status to "occupied"
- Delete `/tables:table_id/seat` updates a table by deleting reservationId and changes status to "free"
</details>

### /reservations
- GET: returns all reservations
- Request body: none
- Response body: 
```JSON
[
    {
        "id": 1,
        "name": "John",
        "date": "2021-08-08",
        "time": "12:00",
        "partySize": 2,
        "phone": "123-456-7890"
    },
    {
        "id": 2,
        "name": "Jane",
        "date": "2021-08-08",
        "time": "12:00",
        "partySize": 2,
        "phone": "123-456-7890"
    }
]
```
- POST: creates a new reservation
- Request body: 
```JSON
{
    "name": "John",
    "date": "2021-08-08",
    "time": "12:00",
    "partySize": 2,
    "phone": "123-456-7890"
}
```
- Response body: 
```JSON
{
    "id": 1,
    "name": "John",
    "date": "2021-08-08",
    "time": "12:00",
    "partySize": 2,
    "phone": "123-456-7890"
}
```
- GET: returns a reservation by id
- Request body: none
- Response body: 
```JSON
{
    "id": 1,
    "name": "John",
    "date": "2021-08-08",
    "time": "12:00",
    "partySize": 2,
    "phone": "123-456-7890"
}
```
- PUT: updates a reservation by id
- Request body: 
```JSON
{
    "id": 1,
    "name": "John",
    "date": "2021-08-08",
    "time": "12:00",
    "partySize": 2,
    "phone": "123-456-7890"
}
```
- Response body: 
```JSON
{
    "id": 1,
    "name": "John",
    "date": "2021-08-08",
    "time": "12:00",
    "partySize": 2,
    "phone": "123-456-7890"
}
```
- DELETE: deletes a reservation by id

### /tables
- GET: returns all tables
- Request body: none
- Response body: 
```JSON
[
    {
        "id": 1,
        "table_name": "#1",
        "capacity": 6,
        "reservation_id": null,
        "status": "free"
    },
    {
        "id": 2,
        "table_name": "#2",
        "capacity": 6,
        "reservation_id": null,
        "status": "free"
    }
]
```
- POST: creates a new table
- Request body: 
```JSON
{
    "table_name": "#1",
    "capacity": 6,
    "reservation_id": null,
    "status": "free"
}
```
- Response body: 
```JSON
{
    "id": 1,
    "table_name": "#1",
    "capacity": 6,
    "reservation_id": null,
    "status": "free"
}
```
- PUT: updates a table by id
- Request body: 
```JSON
{
    "reservation_id": 1
}
```
- Response body: 
```JSON
{
    "id": 1,
    "table_name": "#1",
    "capacity": 6,
    "reservation_id": 1,
    "status": "occupied"
}
```
- DELETE: deletes a table by id


## Installation

- Fork and clone this repository.
- Run cp ./back-end/.env.sample ./back-end/.env.
- Update the ./back-end/.env file with db connections. You can set some up for free with ElephantSQL database instances.
- Run cp ./front-end/.env.sample ./front-end/.env.
- You do not need to make changes to the ./front-end/.env file unless you want to connect to a backend at a location other than http://localhost:5000.
- Run npm install to install project dependencies.
- Run npm run start:dev from the back-end directory to start your server in development mode.- Run npm start from the front-end directory to start the React app at http://localhost:3000.
