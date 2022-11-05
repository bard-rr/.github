<p align="left">
  <img src="https://github.com/bard-rr/.github/blob/main/profile/logo2.png?raw=true" width="400">
</p>
<br/>
 
[![Version](https://img.shields.io/npm/v/bardrr)](https://www.npmjs.com/package/bardrr)
[![Downloads/week](https://img.shields.io/npm/dt/bardrr)](https://npmjs.org/package/bardrr)
[![License](https://img.shields.io/npm/l/monsoon-load-testing.svg)](https://github.com/minhphanhvu/bardrr/blob/master/package.json)

# Outline

- [Description](#Description)
- [Installation](#Installation)
- [Recorder](#Recorder)
- [Replayer](#Replayer)
- [Infrastructure](#Infrastructure)
- [Website](#website)

# Description

Bard is a session replay tool that can be auto-deployed to AWS or set up using a docker-compose. Bard includes a session recorder and a session replayer. This tool will allow you to easily create user conversion funnels and view exactly why a user did not complete the conversion while also identifying sessions that experience errors on the front end of your application.

# Installation

## Prerequisites

- an [AWS account](https://portal.aws.amazon.com/gp/aws/developer/registration/index.html?nc2=h_ct&src=default&tag=soumet-20)
- `npm` is [installed](https://www.npmjs.com/get-npm)
- the AWS CLI is [installed](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html?tag=soumet-20) and configured
- an [AWS named profile](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html)
- the AWS CDK command-line tool is [installed](https://docs.aws.amazon.com/cdk/latest/guide/cli.html?tag=soumet-20)
- Docker is [installed](https://docs.docker.com/get-docker/)

## Recorder

First, install the npm package into your project.
 
```
npm install bardrr
```
 
In your project, import the `Agent` front of the `bardrr` npm package. Then run the `start` method on the Agent passing an object as the argument with
the properties `appName` which will be the name of this specific application, and `endpoint` which is the location of the replayer. Example:
 
```
import Agent from "bardrr"
 
new Agent().start({appName: "Party App", endpoint: "http://www.myfancyapp.com"});
```
 
More Information can be found [Here](https://github.com/bard-rr/agent)

## Replayer

Download the docker compose file on your infrastructure that can be found [Here](https://github.com/bard-rr/deploy).

Run `docker compose up`

The replayer will then be running on port 3003.


# Infrastructure

<p align="center">
  <img src="https://github.com/bard-rr/.github/blob/main/profile/infra.JPG?raw=true" width="600">
</p>

## Agent

The agent acts as the recorder for our application. It collects a snapshot of the original DOM and the events that mutate the DOM to make a recording of the session. These events are correlated with a session ID given to them by the agent. You can learn more [here](https://github.com/bard-rr/agent).

## Agent API

The agent API serves as the ingest point for our application. It first authenticates the agent using JSON web tokens, then begins to collect and parse the session metadata and the events from the agent. The session metadata is stored in the Postgres database while the events moved into the RabbitMQ. You can learn more [here](https://github.com/bard-rr/agent-api).

## Postgres Database

The Postgres Database is used in two distinct ways. First, it is the temporary storage location for the session metadata while the session is still active. Second, it is used as the storage location for funnel information used by the Replayer. You can see the SQL schema [here](https://github.com/bard-rr/deploy/blob/main/postgres_initialization_scripts/bard.sql).

## RabbitMQ

The RabbitMQ is the connection between the Agent API and the Clickhouse Database. The amount of data coming in from the Agent is very large and needs a place to queue while the Clickhouse Database is inserting the data in the event table. RabbitMQ gives the data a place to wait for it to be inserted into the database. You can learn more about RabbitMQ [here](https://www.rabbitmq.com/).

## Session Ender

The Session Ender is a cron job that moves pending sessions from the Postgres database to the Clickhouse database. You can learn more [here](https://github.com/bard-rr/session_ender).

## Clickhouse Database

The Clickhouse Database is the final resting place for all data related to the sessions. It holds all of the metadata and event recordings for all sessions. You can see the Clickhouse schema [here](https://github.com/bard-rr/deploy/blob/main/clickhouse_initialization_scripts/clickhouse_schema.sql).

## Replayer

This is the user interface for our application. The UI allows users to view all sessions, filter sessions based on different criteria, and create user conversion funnels that allow you to know exactly where users fell out of the funnel and did not complete the conversion. You can learn more about Replayer [here](https://github.com/bard-rr/replayer-app).

# Website

You can learn more about us and our tool [here](oursupercoolwebsite.com).