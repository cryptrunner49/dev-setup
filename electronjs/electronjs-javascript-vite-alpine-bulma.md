# Setting up Electron + JavaScript + Vite + Alpine.js + htmx + Bulma + Express + Sequelize + sqlite3

## Creating the Electron project

```bash
npx create-electron-app@latest my-app --template=vite
cd my-app
npm install
```

## Installing alpine.js

```bash
npm install alpinejs
```

### Add the following code to renderer.js

```javascript
import { Alpine } from 'alpinejs';
window.Alpine = Alpine;
Alpine.start();
```

## Installing htmx

```bash
npm install htmx.org@2.0.4
```

### Add the following code to renderer.js

```javascript
import 'htmx.org';
```

## Installing Bulma

```bash
npm install bulma
```

## And import bulma in the index.css

```css
@import 'bulma/css/bulma.css'
```

## Installing Express, Sequelize and sqlite3

```bash
npm install express sequelize sqlite3
```

## Add to main.js

```javascript
import express from 'express';
const expressServer = express();

expressServer.get('/', function (req, res) {
  res.send('Hello World');
});
expressServer.listen(3500);

const { Sequelize } = require('sequelize');
const sequelize = new Sequelize({
  dialect: 'sqlite',
  storage: path.join(__dirname, '../database.sqlite')
});
```

## Add to the createWindow function in main.js

```javascript
try {
  await sequelize.authenticate();
    console.log('Connection has been established successfully.');
} catch (error) {
  console.error('Unable to connect to the database:', error);
}
```

## Starting the app

```bash
npm start
```

## Documentation

[Electron Forge + Vite Template](https://www.electronforge.io/templates/vite-+-typescript)

[Electron Forge Framework Integration with Vue 3](https://www.electronforge.io/guides/framework-integration/vue-3)

[Electron Forge Plugin Vite](https://www.electronforge.io/config/plugins/vite)

[Vue 3 Quick Start Guide](https://vuejs.org/guide/quick-start.html)
