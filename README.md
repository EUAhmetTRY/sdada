# Minecraft Server Status Discord Bot

This simle Discord bot let's you ping your Minecraft server to see if it's online/offline.

Check out the [wiki](https://github.com/TheCactusMonkey/MinecraftServer-DiscordBot/wiki) for more indepth help how to configure your bot using Glitch.com and/or Heroku.com

***

# How to host the bot using Glitch.com

* Click on **New Project** and then on **hello-express** (simple node app).
* Disable the option **Refresh App on Changes**.
* Remove the files: **public/client.js**, **public/style.css**, **views/index.html** (and README.md).
* Now remove everything inside of both **package.json** and **server.js**.
* And put this code into **package.json**.
```
{
  "name": "Server-Status",
  "description": "Minecraft-Server-Status",
  "version": "0.0.0",
  "main": "bot.js",
  "scripts": {
    "start": "node bot.js"
  },
  "engines": {
    "node": "8.4.0"
  },
  "dependencies": {
    "request": "^2.88.0",
    "discord": "^0.8.2",
    "discord.js": "^11.4.2"
  }
}
```
* And put this code into **server.js**.
```
const http = require('http');
const express = require('express');
const app = express();

app.get("/", (request, response) => {
 console.log(Date.now() + " Just got pinged!");
 response.sendStatus(200);
});

app.listen(process.env.PORT);
setInterval(() => {
 http.get(`http://${process.env.PROJECT_DOMAIN}.glitch.me/`);
}, 280000);
```
* Then make a new file called **watch.json** and paste this code inside of the file.
```
{
"install": {
 "include": [
   "^package\\.json$",
   "^\\.env$"
 ]
},
"restart": {
 "exclude": [
   "^public/",
   "^dist/"
 ],
 "include": [
   "\\.js$",
   "\\.json"
 ]
},
"throttle": 600000
}
```
* Now, make a new file called **bot.js** and add everything from the **bot.js** file in this repository.

***

# How to host the bot using Heroku.com
