# Kogito Workshop Devconf.in 2020 

Disclaimer: This workshop is for intermediate level developers.

Table of Contents
=================

* [1) Pre requisites](#1-pre-requisites)
* [2) Clone and Open the kogito travel agency project in VSCode](#2-clone-and-open-the-kogito-travel-agency-project-in-vscode)
* [3) Install the Kogito Extension in VSCode](#3-install-the-kogito-extension-in-vscode)
* [4) Look at the business logic for the Hotel Booking](#4-look-at-the-business-logic-for-the-hotel-booking)
* [5) Look at the business logic for the Flight Booking](#5-look-at-the-business-logic-for-the-flight-booking)
* [6) Look at the business logic for the Travel Request](#6-look-at-the-business-logic-for-the-travel-request)
* [7) Verify the REST Endpoints](#7-verify-the-rest-endpoints)
* [8) Verify the User Interface](#8-verify-the-user-interface)
* [Run the application](#run-the-application)
* [Resources](#resources)

Created by [gh-md-toc](https://github.com/ekalinin/github-markdown-toc)

## 1) Pre requisites

Make sure that you have everything set and installed before continuing:

- [OpenJDK 11+](https://computingforgeeks.com/how-to-install-java-11-openjdk-11-on-rhel-8)
- [VSCode 1.46.0+](https://code.visualstudio.com/docs/setup/linux)
- [Kogito VSCode extension (latest)](https://github.com/kiegroup/kogito-tooling/releases)
- [Red Hat Java VSCode extension (latest)(optional)](https://marketplace.visualstudio.com/items?itemName=redhat.java)
- [Maven 3.6.0+](https://maven.apache.org/install.html)
- [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

## 2) Clone and Open the kogito travel agency project into VSCode

To clone: `git clone git@github.com:manaswinidas/devconfin-2020.git` or you may clone using HTTPS too.

Run the following command on your terminal:

 ```bash
code kogito-travel-agency
```

`kogito-travel-agency` is the project folder.

Alternatively,

1. Open Visual Studio Code
2. Go to "File", "Add Folder to Workspace"
3. Select the Folder `kogito-travel-agency` in your file system
4. Click "Add"

## 3) Install the Kogito Extension in VSCode

Search for Kogito Bundle VSCode extension in Visual Studio Marketplace and install it. Link: https://marketplace.visualstudio.com/items?itemName=kie-group.vscode-extension-kogito-bundle

## 4) Look the business logic for the Hotel Booking

![alt text](kogito-travel-agency/docs/hotelbooking.png)

1. On `src/main/resources/org/acme/travel`, there is a BPMN file named `hotelBooking.bpmn2` for the Hotel booking sub-process. Since you have installed an extension, VSCode will automatically open a BPMN editor for you. Using the BPMN editor, look at the following process attributes (properties panel on right side):

- Process Name: _Hotel Booking_
- Id: _hotelBooking_
- Package: `org.acme.travel`
- Process data:
    Two process variables:
    - Name: _hotel_ Data type (custom): `org.acme.travel.Hotel`
    - Name: _trip_ Data type (custom): `org.acme.travel.Trip`

**Important!** Save your work: ctrl+s (Or cmd+s if you are using mac) in case you make any changes in the BPMN editor.

2. Model Hotel Booking process

 - There is a start node, a service task for executing the `HotelBookingService` bean and an end node.
 - Click on the new service task node and click on Properties on the top right corner:
   -  The name `Book Hotel` has been added;
   -  Click on Implementation/Execution to explore more properties:
     - Implementation is _Java_
     - Interface is the complete name (FQDN) of the `HotelBookingService` class: `org.acme.travel.service.HotelBookingService`
     - Operation is the name of the method that you created in the `HotelBookingService` class service.
     - Assignments(1 input/1 output):
          - Input: Input named _Parameter_ of type (custom) `org.acme.travel.Trip` and source _trip_.
          - Output: Output named _Result_ of type (custom) `org.acme.travel.Hotel` and source _hotel_.

**Important!** Save your work: ctrl+s (Or cmd+s if you are using mac) in case you make any changes in the BPMN editor.

## 5) Look at the business logic for the Flight Booking

![alt text](kogito-travel-agency/docs/flightbooking.png)

1. Inside `src/main/resources/org/acme/travel`, there is another BPMN file named `flightBooking.bpmn2` for the Flight booking sub-process. Using the BPMN editor, have a look at the following process attributes (properties panel on right side):

- Process Name: _Flight Booking_
- Id: _flightBooking_
- Package: `org.acme.travel`
- Process data:
    Two process variables:
    - Name: _flight_ Data type (custom): `org.acme.travel.Flight`
    - Name: _trip_ Data type (custom): `org.acme.travel.Trip`

**Important!** Save your work: ctrl+s (Or cmd+s if you are using mac) in case you make any changes in the BPMN editor.

2. Model Flight Booking process

 - There is a start node, a service task for executing the `FlightBookingService` bean and an end node.
 - Click on the new service task node and click on Properties on the top right corner:
   - Name is set as _Book flight_ 
   - Click on Implementation/Execution to explore more properties:
     - Implementation is _Java_
     - Interface is the fully complete name of the `FlightBookingService` class: `org.acme.travel.service.FlightBookingService`
     - Operation is the name of the method that you created in the `FlightBookingService` class service.
     - Assignments(1 input/1 output):
          - Input: Input named _Parameter_ of type `org.acme.travel.Trip` and source _trip_.
          - Output: Output named _Result_ of type `org.acme.travel.Flight` and source _flight_.

**Important!** Save your work: ctrl+s (Or cmd+s if you are using mac) in case you make any changes in the BPMN editor.

## 6) Look at the business logic for the Travel Request

![alt text](kogito-travel-agency/docs/travels.png)

1. Inside `src/main/resources/org/acme/travel`, there is a BPMN file for the Travels process called `travels.bpmn2`. Using the BPMN editor, have a the following process attributes (properties panel on right side):

- Process Name: _Travels_
- Id: _travels_
- Package: `org.acme.travel`
- Process data (Process variables):
    - Name: _flight_ Data type (custom): `org.acme.travel.Flight`
    - Name: _trip_ Data type (custom): `org.acme.travel.Trip`
    - Name: _hotel_ Data type (custom): `org.acme.travel.Hotel`
    - Name: _traveller_ Data type (custom): `org.acme.travel.Traveller`

**Important!** Save your work: ctrl+s (Or cmd+s if you are using mac) in case you make any changes in the BPMN editor.

2. Model Travel process

- There is a start node which leads to _Visa Check_ rule node with the following attributes:
    - Name: _Visa Check_
    - Implementation/Execution
        - Rule Language: _DRL_
        - Rule Flow Group (new): _visas_
    - Data Assignments( 2 inputs and 1 output)
      - Input:
        - Input named _trip_ of type (custom) `org.acme.travel.Trip` and source _trip_.
        - Input named _traveller_ of type (custom) `org.acme.travel.Traveller` and source _traveller_.
      - Output:
        - Output named _trip_ of type `org.acme.travel.Trip` and target _trip_.

**Important!** Save your work: ctrl+s (Or cmd+s if you are using mac) in case you make any changes in the BPMN editor.

- From _Visa Check_, there is an exclusive gateway
- From the exclusive gateway, there is a user task named _Visa Application_ with the following attributes
    - Implementation/Execution, Task Name: _VisaApplication_
- Click on the connecting arrow between the exclusive gateway and the _Visa Application_ task and there is this attribute:
    - Implementation/Execution,  Expression radio button:
    ```java
        return trip.isVisaRequired();
    ```
- There is another exclusive gateway and connection between both nodes _Visa Application_ and previous exclusive gateway, creating a fork in the process model.
- Select the connecting arrow between both exclusive gateways and there is this attribute:
    - Implementation/Execution, Expression radio button:
    ```java
        return !trip.isVisaRequired();
    ```
- From the newly created exclusive gateway, there is a new parallel gateway.
- From the parallel gateway, there is a new reusable sub-process for _Book Hotel_ process with the following attributes:
  - Implementation/Execution, Called Element (new): _hotelBooking_
  - Data Assignments
    - Input: Input named _trip_ of type (custom) `org.acme.travel.Trip` and source _trip_.
    - Output: Output named _hotel_ of type `org.acme.travel.Hotel` and source _hotel_.

**Important!** Save your work: ctrl+s (Or cmd+s if you are using mac) in case you make any changes in the BPMN editor.

- From the parallel gateway, there is a new reusable sub-process for _Book Flight_ process with the following attributes:
  - Implementation/Execution, Called Element (new): _flightBooking_
  - Data Assignments
    - Input: Input named _trip_ of type (custom) `org.acme.travel.Trip` and source _trip_.
    - Output: Output named _flight_ of type (custom) `org.acme.travel.Flight` and source _flight_.
 
**Important!** Save your work: ctrl+s (Or cmd+s if you are using mac) in case you make any changes in the BPMN editor.

- There is a new parallel gateway and connection between both reusable sub-process nodes into it.
- From the parallel gateway, there is a new user task named _Confirm Travel_ with the following attributes:
    - Task Name: _ConfirmTravel_
- The _Confirm Travel_ leads to an end node.

**Important!** Save your work: ctrl+s (Or cmd+s if you are using mac) in case you make any changes in the BPMN editor.

To test your process, uncomment the tests ([CTRL+K, CTRL+U](https://stackoverflow.com/questions/5717816/how-to-uncomment-multiple-lines-of-code-in-visual-studio/5717871) or CMD+K,CMD+U when using a mac) on `src/test/java/org/acme/travel/TravelTest.java` and execute:

```bash
mvn clean verify
```

Your test will fail because the assertions are expecting fixed values that are being returned from your services. Make sure to fix your services and try again.

## 7) Verify the REST Endpoints

1. Run the following command to execute your Kogito application:

```bash
mvn clean quarkus:dev
```

2. Verify travels endpoint:

```bash
curl -X GET http://localhost:8080/travels
```

Should return an empty array since you don’t have any travels yet.

3. Post new Travel that **does not** require visa

```bash
curl -H "Content-Type: application/json" -H "Accept: application/json" -X POST http://localhost:8080/travels -d @- << EOF
{
    "traveller" : {
        "firstName" : "John",
        "lastName" : "Doe",
        "email" : "john.doe@example.com",
        "nationality" : "American",
        "address" : {
            "street" : "main street",
            "city" : "Boston",
            "zipCode" : "10005",
            "country" : "US"
        }
    },
    "trip" : {
        "city" : "New York",
        "country" : "US",
        "begin" : "2019-12-10T00:00:00.000+02:00",
        "end" : "2019-12-15T00:00:00.000+02:00"
    }
}
EOF
```

Make note of the returned `id` field, since your will need it from now on.

4. Get open tasks for current process, should return `ConfirmTravel` (replace `{uuid}` with the `id` field returned in the previous step):

```bash
curl -X GET http://localhost:8080/travels/{uuid}/tasks
```

Make note of the returned `id` field, since your will need it from now on in the `task-uuid` placeholders.

5. Completes confirms travel task - meaning confirms (and completes) the travel request:

Replace `{uuid}` with the `id` returned from the step #3 and `{task-uuid}` with the id from the previous step (#4):

```bash
curl -H "Content-Type: application/json" -H "Accept: application/json" -X POST http://localhost:8080/travels/{uuid}/ConfirmTravel/{task-uuid} -d '{}'
```

You should receive a reply similar to this one:

```json
{"id":"966aa8a3-0e3f-4263-8e0e-780170e846e5","flight":{"flightNumber":"MX555","seat":"34B","gate":"C4","departure":1575928800000,"arrival":1575928800000},"trip":{"city":"New York","country":"US","begin":1575928800000,"end":1576360800000,"visaRequired":false},"hotel":{"name":"Perfect hotel","address":{"street":"34 Great Streat","city":"New York","zipCode":"05644","country":"US"},"phone":"09876543","bookingNumber":"XX-012345","room":"69"},"traveller":{"firstName":"John","lastName":"Doe","email":"john.doe@example.com","nationality":"American","address":{"street":"main street","city":"Boston","zipCode":"10005","country":"US"}}}
```

6. Verify process has finished (replace `{uuid}` with the same `id` from the travels endpoint)

```sh
curl -X GET http://localhost:8080/travels/{uuid}
```

You’ll receive an empty response, the process has finished and there’s no reason to keep the travel anymore.

7. Post new Travel that **does** require visa

```sh
curl -H "Content-Type: application/json" -H "Accept: application/json" -X POST http://localhost:8080/travels -d @- << EOF
{
    "traveller" : {
        "firstName" : "Jan",
        "lastName" : "Kowalski",
        "email" : "jan.kowalski@example.com",
        "nationality" : "Polish",
        "address" : {
            "street" : "polna",
            "city" : "Krakow",
            "zipCode" : "32000",
            "country" : "Poland"
        }
    },
    "trip" : {
        "city" : "New York",
        "country" : "US",
        "begin" : "2019-12-10T00:00:00.000+02:00",
        "end" : "2019-12-15T00:00:00.000+02:00"
    }
}
EOF
```

Make note of the returned `id` field, since your will need it from now on.

8. Get open tasks for current process, should return `VisaApplication` (replace `{uuid}` with the `id` field returned in the previous step):

```sh
curl -X GET http://localhost:8080/travels/{uuid}/tasks
```

Make note of the returned `id` field, since your will need it from now on in the `task-uuid` placeholders.

9. Completes Visa Application request. Replace `{uuid}` with the `id` returned from the step #7 and `{task-uuid}` with the id from the previous step (#8):

```sh
curl -H "Content-Type: application/json" -H "Accept: application/json" -X POST http://localhost:8080/travels/{uuid}/VisaApplication/{task-uuid} -d '{}'
```

10. Get open tasks for current process, should return `ConfirmTravel`. Replace `{uuid}` with the travel `id`:

```sh
curl -X GET http://localhost:8080/travels/{uuid}/tasks
```

11. Completes confirms travel task - meaning confirms (and completes) the travel request. Replace the ids placeholders accordingly:

```sh
curl -H "Content-Type: application/json" -H "Accept: application/json" -X POST http://localhost:8080/travels/{uuid}/ConfirmTravel/{task-uuid} -d '{}'
```

12. Verify process has finished:

```sh
curl -X GET http://localhost:8080/travels/{uuid}
```

You’ll receive an empty response, the process has finished and there’s no reason to keep the travel anymore.

## 8) Verify the User Interface

Explore Swagger UI on http://localhost:8080/swagger-ui/

Plan new travel requests using the Travel Agency UI available on http://localhost:8080/

## Run the application

Run the application:

```bash
cd devconfin-2020/kogito-travel-agency
mvn clean verify quarkus:dev
```

## Resources

- [Kogito Wiki](https://github.com/kiegroup/kogito-runtimes/wiki)
- [More about creating projects using Kogito](https://docs.jboss.org/kogito/release/latest/html_single/#proc-kogito-creating-project_kogito-creating-running)
- [Workshop Feedback - we want to hear back from you](https://forms.gle/ow6PbxT7zuqXCjrt8)
