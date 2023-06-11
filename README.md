# LearningJavascript
Notes for nodeJS

DEV TOOLS
	npm i -D nodeamon
		- To Restart Project On Change
	npm i -D browser-sync
		- To Refresh Browser On Change ( Happens only on new port not on the original port )
	npx browser-sync init
		- To initialize bs-config.js file so that configurations can be mentioned that is - like change in which file will trigger the reload on browser
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
bs-config.json
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
module.exports = {
    proxy: "localhost:8000",
    files: ["**/*.css", "**/*.pug", "**/*.js"],
    ignore: ["node_modules"],
    reloadDelay: 10,
    ui: false,
    notify: false,
    port: 3000,
  };
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
package.json
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
{
  "name": "node",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "nodemon ./index.js",
    "ui": "browser-sync start --config bs-config.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "-": "^0.0.1",
    "express": "^4.18.2",
    "pug": "^3.0.2"
  },
  "devDependencies": {
    "browser-sync": "^2.29.3",
    "nodemon": "^2.0.22"
  }
}


In NodeJS Or Javascript
 if we write require("./filenamewithpath");
it will execute all the lines written in the files scope (if not function that has not been called inside that file itself)


Basic Coding Structure For Beginning To Understand NodeJS along with PUG and Express

// index.js
//---------------------------------------------------------------------------------
/**
 * Required External Modules
 */
//---------------------------------------------------------------------------------
const express = require("express");
const path = require("path");
//---------------------------------------------------------------------------------
//---------------------------------------------------------------------------------
/**
 * App Variables
 */
//---------------------------------------------------------------------------------
const app = express();
const port = process.env.PORT || 8000; 
//---------------------------------------------------------------------------------
//---------------------------------------------------------------------------------
/**
 *  App Configuration
 */
//---------------------------------------------------------------------------------
// app.get("/", (req,res) => {
//     res.status(200).send("HELLO");
// });
app.get("/", (req, res) => {
    res.render("index", { title: "Home" });
  });
app.set("views", path.join(__dirname, "views"));
app.set("view engine", "pug");
app.use(express.static(path.join(__dirname, "public")));
//---------------------------------------------------------------------------------
//---------------------------------------------------------------------------------
/**
 * Routes Definitions
 */
//---------------------------------------------------------------------------------
app.listen(port, () => {
    console.log(`listening to http://localhost:${port}`);
});

app.get("/user", (req, res) => {
    res.render("user", { title: "Profile", userProfile: { nickname: "Soumya" } });
  });
  app.get("/logout", (req, res) => {
    res.redirect("/");
  });
/**
 * Server Activation
 */
//---------------------------------------------------------------------------------
//---------------------------------------------------------------------------------
app.set("views", path.join(__dirname, "views"));
app.set("view engine", "pug");
//---------------------------------------------------------------------------------
