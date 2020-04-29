# db-fixture-rest-api

A REST API for loading and unloading MongoDB database fixtures.

Featured in the book [Bootstrapping Microservices](http://bit.ly/2o0aDsP).

## **Don't run this on a production server, it is for testing only and provides unauthenticated access to your database!**

Use this in your automated test process to load and unload your database for testing.

This builds upon [node-mongodb-fixtures](https://www.npmjs.com/package/node-mongodb-fixtures).

**Scroll** to the end to see how you can support the developer.

## Pre-requisites

You must have Node.js installed to run this.

You need a MongoDB instance ready for testing.

## Important files

    src/index.js                -> The JavaScript file that implements the REST API.
    Dockerfile                  -> Allows you to package this application in a Docker image.
    fixtures/                   -> Database fixtures live under this directory.
        example-json-fixture/   -> An example database fixture in JSON format.
        example-js-fixture/     -> An example database fixture in JavaScript format.

## REST API endpoints

This REST API exposes the following endpoints.

The default port number is 3555, but you can set this to any value as described in the section *Use it in your project* below.

### Load fixture

    HTTP GET http://localhost:3555/load-fixture?db=<database-name>&fix=<fixture-to-load>

### Unload fixture

    HTTP GET http://localhost:3555/unload-fixture?db=<database-name>&ix=<fixture-to-unload>


### Retrieve a database collection

    HTTP GET http://localhost:3555/get-collection?db=<database-name>&col=<collection-to-get>

### Drop a database collection

    HTTP GET http://localhost:3555/drop-collection?db=<database-name>&col=<collection-to-drop>

**Be careful to only drop a collection on dev or testing machines!**

### Drop a database

    HTTP GET http://localhost:3555/drop-database?db=<database-name>

**Be careful to only drop a database on dev or testing machines!**

## Auto reload

By default the db fixture REST API is executed using [nodemon](https://nodemon.io/) and is setup to watch the fixtures directory. This means you can update or add fixtures in order to restart the server.

## Trial run

Clone or download this repo. Open a command line and change directory to the repo then install dependencies:

    cd db-fixture-rest-api
    npm install

Now run the REST API:

    npm start

Now use curl or your fav REST API client (eg [ARC](https://install.advancedrestclient.com) or [Postman](https://www.getpostman.com/)), hit the HTTP endpoints documented in the previous section to load and unload your database fixtures.

Two example database fixtures are included under the *fixtures* sub-directory.

You can load them using the names *example-js-fixture* and *example-json-fixture*.

For example, to load *example-js-fixture* hit http://localhost:3555/load-fixture?db=my-test-db&fix=example-json-fixture with a HTTP GET request.

After you have loaded a fixture, browse your database to check that the data has been loaded correctly. By default it is loaded under a database named *my-test-database*.

After that you can unload the fixture and then check that the data was removed from the database.

For example to unload *example-js-fixture*, hit http://localhost:3555/unload-fixture?db=my-test-db&fix=example-json-fixture with a HTTP GET request.

You can also directly drop any collection, for example to drop a collection called *person*, hit http://localhost:3555/drop-collection?db=my-test-db&col=person with a HTTP GET request. 

In a similar way you can drop an entire database.

## Use it in your project

To use this REST API to help test your own project please customize it by setting the following environment variables:

- FIXTURES_DIR - Set the location of the fixtures directory (defaults to 'fixtures').
- PORT - Set the port number of the REST API (defaults to 3555).
- DBHOST - Set the host address for the MongoDB server instance (defaults to mongodb://localhost:27017)..

Doesn't do what you want?
Please fork the code and hack it to your heart's content ;)

## Going further

Please see [node-mongodb-fixtures](https://www.npmjs.com/package/node-mongodb-fixtures) for more of what you can do with these database fixtures.

## Supporting the developer

<a class="support" target="_blank" href="https://www.data-forge-notebook.com/"><img src="images/support1.png"></a>

<a class="support" target="_blank" href="http://bit.ly/2t2cJu2"><img src="images/support2.png"></a>

<a class="support" target="_blank" href="http://bit.ly/2t2cJu2"><img src="images/support3.png"></a>
