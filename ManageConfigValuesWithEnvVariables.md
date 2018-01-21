## Manage Configuration Values with Environmnet Variables
It can be useful to store your environment variables in a separate config file to make them easy to update, reference, and delete when building your app. In Node, we reference environment variabes using the template `process.env.ENV_VARIABLE`. You can then pass environment variables when starting your script i.e.:

```bash
MONGO_URI=mongodb://localhost:27017/foo node ./server/index.js
```

An easier way to manage environment variables is through a `.env` file.

```
// .env file
MONGO_URI=mongodb://localhost:27017/foo
```

To access variables in a `.env` file, we need to use the `dotenv` package.

```bash
yarn add dotenv
```

Then, at the top of our script, call the `config` function on it. This will look for a `.env` file in the root directory and inject the listed environmnet variables.

```javascript
require("dotenv").config();
// rest of your code now has access to environment variables
```