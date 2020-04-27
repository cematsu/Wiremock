![Wiremock](assets/intro.png "Wiremock Intro")

Wiremock - API Mock Server
=======

Mock your APIs for fast, robust and comprehensive testing
WireMock is a simulator for HTTP-based APIs. Some might consider it a service virtualization tool or a mock server.
It enables you to stay productive when an API you depend on doesn't exist or isn't complete. It supports testing of edge cases and failure modes that the real API won't reliably produce. And because it's fast it can reduce your build time from hours down to minutes.

----------
How wiremock works
----------

In this example we're using a stand alone java version of wiremock that will create a mock server locally.
With wiremock you can create requests through files in the "mappings" folder or you can create the requests through HTTP requests (post)

![Mappings](assets/mappings.png "Create mocks with files")

![Create request during runtime](assets/createRequest.png "Create mocks during runtime")

----------
Wiremock Example - Starting wiremock
----------

To go through this example follow the steps below
Create a folder in your computer to store the example files
Open the command line and navigate to that folder
run the command below:

    git clone https://github.com/cematsu/Wiremock.git

on the command line start wiremock using the command below:

    java -jar wiremock-standalone-2.24.1.jar --port 7777

Wiremock server should be up and running using the port 7777

![Wiremock started](assets/mappings.png "Wiremock Started")

----------
Wiremock Example - pre existing mappings
----------

To work with wiremock you need to send HTTP Requests, in this example we will use postman
On postman import the Collection in the postman folder and execute the first request "get example" inside the "Pre configured mocks"
you should receive a response like this:

    {
        "name": "Galaxy S9",
        "brand": "Samsung",
        "region": "EMEA",
        "Price": 100.0,
        "Id": "999"
    }

Verify that this mock was created using a file located in the "mappings" folder. The file is named as "CT001-GetProduct.json"

    "request": {
        "url": "/product/999",
        "method": "GET"
     }

Request object is were you define the endpoint that needs to be mocked and the method (Post, Get, Patch, Put, Delete...)

    "response": {
    "status": 200,
    "jsonBody": {
    	"name": "Galaxy S9",
    	"brand": "Samsung",
    	"region": "EMEA",
    	"Price": 100.00,
    	"Id": "999"
    }
The response object is where you define the body and the HTTP response

    "headers": {
        "Content-Type": "application/json"
    }

You can specify the headers of your requests in the "header" object

----------
Wiremock Example - Creating a mock on the fly
----------
On postman navigate to the "Mock Management" folder, there you can find examples to create and use mocks on runtime

![Create request during runtime](assets/createRequest.png "Create mocks during runtime")

Wiremock uses HTTP standards so use Post to create requests, Patch or Put to update requests, Get to list the requests and delete to delete requests

----------
Wiremock Management
----------

Wiremock runs as a background process and all of it's management is done through HTTP requests.
On postman in the "Wiremock Management" folder you can find a few examples of management requests

To shutdown wiremock

    http://localhost:7777/__admin/shutdown

To List the latest requests

    http://localhost:7777/__admin/requests

To List all mocks

    http://localhost:7777/__admin/mappings


For more information please see:
http://wiremock.org/docs/stubbing/
