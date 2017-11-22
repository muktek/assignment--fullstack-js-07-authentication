# Full Stack JS Project - Authentication Part 1
**`fullstack-js-07--auth-part-1`**


## Context
You are going to build a full stack web application with node.js + React. In order to become familiar with how a node project works, you will be responsible for configuring the  initial major components of the project.  

- express server
- application routes
- views
- api layer
  - data access
  - data models + relations (ORM)
  - RESTful routes
  - authentication
    - **initial configuration [this assignment]**
    - application integration
  - React
    - initial configuration
    - application api integration
    - application auth integration


## The Assignment
For this assignment, we will focus on configuring the application's **Authentication** feature. Authentication allows our application to *verify the identity* of a user and permit or prohibit actions accordingly.

###  Overview
You will need to configure the application so that a user can authenticate by using the following routes:

*NOTE:* You will need to test the routes in Postman to confirm you've configured correctly.

```
POST - `/auth/register`  - Creates a new user + password
  application/json body:
    {"email" : "...", "password" : "..."}

POST - `/auth/login`     - A user authenticates with user + password
  application/json body:
    {"email" : "...", "password" : "..."}

GET  - `/auth/logout`    - Logs out a user

GET  - `/auth/current`   - Checks for a user's current authenticated session.
```



### Requirements
In order to complete this assignment, you will need to:

- [x] **Download + Install Postman request client**
  - https://www.getpostman.com/

- [x] **Install yeoman + nxkplus generator**
  ```sh
  npm install -g yo
  npm install -g generator-nxkplus

  # check for prompt
  yo nxkplus
  ```

- [x] **Run the nxkplus authentication generator**
  ```sh
  yo nxkplus:auth
  ```

- [x] **Import the libraries + middleware**
  ```js
  const passport = require('passport')
  const cookieSession = require('cookie-session')
  const cookieParser = require('cookie-parser')

  const registerLocalStrategy = require('./src/middleware/passport-local--registerLocalStrategy.js')
  const { configDeserializeUser, configSerializeUser } = require('./src/helpers/passport-local--sessionActions.js')
  ```

- [x] **Configure libraries + middleware w/ application**
  ```js
  // Cookie Parse + Cookie Session middleware
  app.use(cookieParser())
  app.use(cookieSession({
    name: 'cookiemonster',
    secret: 'superdupersupersecret',
    httpOnly: true,
    signed: false
  }))

  // Passport middleware
  app.use(passport.initialize())
  app.use(passport.session())
  passport.use(registerLocalStrategy())
  passport.serializeUser(configSerializeUser())
  passport.deserializeUser(configDeserializeUser())
  ```

- [x] **Import `authRouter.js` and create router middleware**
  ```js
  const authRouter = require('./src/routes/authRouter.js')

  ...

  app.use('/auth', authRouter)
  ```

+ [x] **Test Routes in [Postman]()**
  + POST - `/auth/register`
    + application/json body:
    ```
    {"email" : "testeracct@mail.com", "password": "1234"}
    ```
  + POST - `/auth/login`
    + application/json body:
    ```
    {"email" : "testeracct@mail.com", "password": "1234"}
    ```

  + GET - `/auth/login`

  + GET - `/auth/logout`

## Setup Instructions

In Terminal:

```sh
# (1) navigate to your project--devjobs directory
cd ~/Documents/muktek/assignments/project--devjobs

# (2) Commit your changes from the previous demo
git add .
git commit -m 'committing work from part-06-rest-api'

# (3) You will work on the part-07-auth-part-1 branch for this feature
git checkout -b part-07-auth-part-1

```
