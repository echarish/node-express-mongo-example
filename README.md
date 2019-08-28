# Nodejs Express Mongoose Demo

This is a demo application illustrating various features used in everyday web development, with a fine touch of best practices. The demo app is a blog application where users can signup, create an article, delete an article and add comments etc.

Table of contents:

<!-- TOC depthFrom:2 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Nodejs Express Mongoose Demo](#nodejs-express-mongoose-demo)
  - [Boilerplate](#boilerplate)
  - [Install](#install)
  - [Tests](#tests)
  - [Docker](#docker)
  - [Expose DB on GCP](#expose-db-on-gcp)

<!-- /TOC -->

## Boilerplate

Want to build something from scratch? use the [boilerplate](https://github.com/madhums/node-express-mongoose)

* Checkout the [apps that are built using this approach](https://github.com/madhums/node-express-mongoose/wiki/Apps-built-using-this-approach)
* The [wiki](https://github.com/madhums/node-express-mongoose/wiki) is wip, it has some information about the way application is setup.

## Install

```sh
git clone git://github.com/madhums/node-express-mongoose-demo.git
npm install
cp .env.example .env
npm start
```

Then visit [http://localhost:3000/](http://localhost:3000/)

**NOTE:** Do not forget to set the twitter, google, linkedin and github `CLIENT_ID`s and `SECRET`s. In `development` env, you can set the env variables in `.env` and replace the values there. In `production` env, it is not safe to keep the ids and secrets in a file, so you need to set it up via commandline. If you are using heroku checkout how environment variables are set [here](https://devcenter.heroku.com/articles/config-vars).

## Tests

```sh
npm test
```

## Docker

You can also use docker for development. Make sure you run npm install on your host machine so that code linting and everything works fine.

```sh
npm i
cp .env.example .env
```

Start the services

```sh
docker-compose up -d
```

View the logs

```sh
docker-compose logs -f
```

In case you install a npm module while developing, it should also be installed within docker container, to do this first install the module you want with simple `npm i module name`, then run it within docker container

```sh
docker-compose exec node npm i
```

If you make any changes to the file, nodemon should automatically pick up and restart within docker (you can see this in the logs)

To run tests

```sh
docker-compose exec -e MONGODB_URL=mongodb://mongo:27017/noobjs_test node npm test
```

Note that we are overriding the environment variable set in `.env` file because we don't want our data erased by the tests.

Note: The difference between exec and run is that, exec executes the command within the running container and run will spin up a new container to run that command. So if you want to run only the tests without docker-compose up, you may do so by running `docker-compose run -e MONGODB_URL=mongodb://mongo:27017/noobjs_test node npm test`

## Expose DB on GCP
go to your VPC firewall

https://console.cloud.google.com/networking/firewalls

and create a firewall rule to allow traffic on your desired tcp port

Create a Firewall Rule for SQL Server Configure a firewall rule to allow traffic on port 1433 so other clients can connect to the newly created SQL Server instance over the public internet:

In the Developers Console main menu, go to the Firewall rules section.

OPEN THE FIREWALL RULES

Click the Add firewall rule button.

Name the new firewall rule allow-tcp-1433.

Set Source Filter to IP Ranges.

For Source IP Ranges enter *0.0.0.0/0* This value allows access by all IP addresses.

Warning: This configuration leaves your SQL Server instance open to traffic from everyone, everywhere. It is used only for demonstration purposes. In production environments, restrict access to only those IP addresses that need access. For Allowed protocols and ports enter tcp:1433. Click the Create button to create the firewall rule.
