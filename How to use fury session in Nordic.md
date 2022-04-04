# How to use fury session in Nordic

## Introduction

This documentation is intended to help you use the fury session in Nordic.

## Prerequisites

Must have writing privileges on the project and session.

## Directions

The step by step that we are going to do is the following:

1) Configure session middleware in project config.
2) Activate the session service in Fury.

### Step 1: Configure session middleware in project config ("/config/default.js").

This must be done from the project settings, as Nordic implements it internally. The configuration file "/config/default.js" should look like the one in [this repo](https://github.com/mercadolibre/fury_navigation-frontend/blob/master/config/default.js)

### Step 2: Activate the session service in Fury.

This must be done from the Fury frontend, in the session section, for the scopes that are needed:

![1](https://user-images.githubusercontent.com/81833300/161579797-1fccb3b2-9877-4f3a-8470-0f70a4a0feaf.png)

![2](https://user-images.githubusercontent.com/81833300/161579816-1bfe5365-c069-4b56-a3b3-8328046879a7.png)
