# **Rest Booking API Testing with Postman Newman:**

This project demonstrates API testing using Postman, providing a collection of tests to validate various endpoints of the API.



# **Features:**

- Tests for GET, POST, PUT, DELETE requests
- Collection of tests covering different API endpoints
- Environment setup for easy switching between environments
- Pre-request scripts for data setup
- Test scripts for assertions and validations



# **API Documentation:**
[https://documenter.getpostman.com/view/13082503/2sA2xmUAJ1](https://documenter.getpostman.com/view/13082503/2sA2xmUAJ1)



# **Technology used:**
- Postman
- Newman



# **Prerequisite:**
- Node Js
- Newman
- Newman Html Report Library

# **Installation:**
1. Postman: If you haven't already, [download and install Postman.](https://www.postman.com/downloads/)
2. Clone the repository:
https://github.com/KanizFatema0/API-Testing-of-REST-Booking-with-Postman-with-Newman-Report.git
3. Import the Postman collection:
- Open Postman.
- Click on the Import button.
- Select the file from the repository.
4. Import the Postman environment:
- In Postman, click on the gear icon in the top right corner.
- Select Import and choose the file.
5. Newman and Report Installation Process:
- Newman Install Command:
 ```npm install -g newman```
- Newman Html Report Install Command:
 ``` npm install -g newman-reporter-htmlextra```

# **Usage:**
1. Select Environment:
- In Postman, select the appropriate environment (e.g., Development, Production) from the top-right dropdown.
2. Run Collection:
- Select the imported collection from the Collections sidebar.
- Click on the Runner button to open the collection runner.
- Select the desired environment.
- Click Start Test to run the collection.
3. View Results:
- Once the tests are complete, view the results in the Runner tab.
- Detailed test results can be viewed for each request.

# **Testing:**

# **Test Case Scenarios:**

# **1.Create New Booking:**

**Request URL: https://restful-booker.herokuapp.com/booking/**

Request Method: POST

Pre- request Script:
```
//First Name

var firstName = pm.variables.replaceIn("{{$randomFirstName}}")
pm.environment.set("firstName",firstName)

//Last Name

var lastName = pm.variables.replaceIn("{{$randomLastName}}")
console.log(lastName)
pm.environment.set("lastName",lastName)

//Total Price

var totalPrice = pm.variables.replaceIn("{{$randomInt}}")
console.log(totalPrice)
pm.environment.set("totalPrice",totalPrice )

//Deposit Paid

var depositPaid = pm.variables.replaceIn("{{$randomBoolean}}")
console.log(depositPaid)
pm.environment.set("depositPaid",depositPaid )


//checkin Date

const moment = require('moment')
const today = moment()
var checkIn = today.add(1,'d').add(3,'M').format("YYYY-MM-DD")
pm.environment.set("checkIn",checkIn)

//checkout Date

var checkOut = today.add(2,'d').add(3,'M').format("YYYY-MM-DD")
pm.environment.set("checkOut",checkOut)
```
 Request Body 
```
{
	"firstname" : "{{firstName}}",
	"lastname" : "{{lastName}}",
	"totalprice" : "{{totalPrice}}",
	"depositpaid" : "{{depositPaid}}",
	"bookingdates" : {
    	"checkin" : "{{checkIn}}",
    	"checkout" : "{{checkOut}}"
	},
	"additionalneeds" : "Breakfast"
}
```
Response Body 

```
{
    "bookingid": 2571,
    "booking": {
        "firstname": "Yessenia",
        "lastname": "Crist",
        "totalprice": 451,
        "depositpaid": true,
        "bookingdates": {
            "checkin": "2025-03-01",
            "checkout": "2025-06-03"
        },
        "additionalneeds": "Breakfast"
    }
}
```
# **Get Booking Details By ID**

**Request URL: https://restful-booker.herokuapp.com/booking/**

Request Method: GET

Request Body:
```
{
    "firstname": "Ervin",
    "lastname": "Cremin",
    "totalprice": 107,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2025-02-28",
        "checkout": "2025-06-02"
    },
    "additionalneeds": "Breakfast"
}
```
# ** 3. Create A Token For Authentication **

** Request URL: https://restful-booker.herokuapp.com/auth **

Request Method: POST

Pre-request Script: None

Request Body:

```
var jsonData = pm.response.json()

pm.environment.set("access token",jsonData.token)
```
Response Body:
```
{
   "token": "06eb798bf6f2caa"
}
```
# ** 4. Update the Booking Details **
**Request URL: https://restful-booker.herokuapp.com/booking/bookingid**

Request Method: PUT

Pre-request Script:

```
//updated first name
var updated_firstName = pm.variables.replaceIn("{{$randomFirstName}}")

pm.environment.set("updated_firstName",updated_firstName)

//updated lastname

var updated_lastName = pm.variables.replaceIn("{{$randomLastName}}")

pm.environment.set("updated_lastName",updated_lastName)

//updated total price

var  updated_totalPrice = pm.variables.replaceIn("{{$randomInt}}")

pm.environment.set("updated_totalPrice", updated_totalPrice)

//updated deposit paid

var  updated_depositPaid = pm.variables.replaceIn("{{$randomBoolean}}")

pm.environment.set(" updated_depositPaid", updated_depositPaid)

//updated check-in

const moment = require('moment')
const today = moment()

var  updated_checkIn = today.add(1, 'd').add(3, 'M').format("YYYY-MM-DD")
pm.environment.set("updated_checkIn", updated_checkIn)

//updated check-out

const moments = require('moment')

const tomorrow = moments()

var updated_checkOut = tomorrow.add(2, 'd').add(3, 'M').format("YYYY-MM-DD")

pm.environment.set("updated_checkOut",updated_checkOut)

```
Request Body:

```
{
	"firstname" : "{{updated_firstName}}",
	"lastname" : "{{updated_lastName}}",
	"totalprice" : "{{updated_totalPrice}}",
	"depositpaid" : "{{updated_depositPaid}}",
	"bookingdates" : {
    	"checkin" :"{{updated_checkIn}}",
    	"checkout" : "{{updated_checkOut}}"
	},
	"additionalneeds" : "Breakfast"
}

```

Response Body:

```
{
    "firstname": "Angel",
    "lastname": "Mills",
    "totalprice": 769,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2025-02-28",
        "checkout": "2025-03-01"
    },
    "additionalneeds": "Breakfast"
}
```
# ** 5. Delete the Booking Details **
**Request URL: https://restful-booker.herokuapp.com/booking/bookingid**

Request Method: DELETE

Response Body: None

Request Body:

```
{
	"firstname" : "Raisa",
	"lastname" : "Fatema",
	"totalprice" : 111,
	"depositpaid" : true,
	"bookingdates" : {
    	"checkin" : "2018-01-01",
    	"checkout" : "2019-01-01"
	},
	"additionalneeds" : "Breakfast"
}

```

# **Run Command**
- Run command for Console:
```
kaniz@MacBook-Pro-3 PostmanProject % newman run PostmanProject.postman_collection.json -e PostmanProject.postman_environment.json
  ```
- Run command for Report:
```
kaniz@MacBook-Pro-3 PostmanProject % newman run PostmanProject.postman_collection.json -e PostmanProject.postman_environment.json -r htmlextra
```

# **Newman Report Summary**
<img width="551" alt="Screenshot 2024-11-30 at 3 13 07 PM" src="https://github.com/user-attachments/assets/6dc51e1a-3554-4973-acb1-54b2c01bff66">
<img width="551" alt="Screenshot 2024-11-30 at 3 13 27 PM" src="https://github.com/user-attachments/assets/7f1385f9-8106-483b-a839-8ca5f5aee2cf">
<img width="551" alt="Screenshot 2024-11-30 at 3 13 43 PM" src="https://github.com/user-attachments/assets/ef5e5d9d-c776-4aa1-815b-99a1219a5702">
<img width="551" alt="Screenshot 2024-11-30 at 3 13 55 PM" src="https://github.com/user-attachments/assets/ef6774f5-c0d3-4d50-af16-1dd0f95d7634">











