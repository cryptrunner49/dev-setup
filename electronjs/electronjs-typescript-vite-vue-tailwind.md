# Setting up Electron + TypeScript + Vite + Vue + Tailwind

## Creating the Electron project

```bash
npx create-electron-app@latest my-app --template=vite-typescript
cd my-app
npm install
npm install vue
npm install --save-dev @vitejs/plugin-vue
```

## Creating the Vue project

```bash
npm create vue@latest
```

### Vue project options

```bash
✔ Project name: vue
✔ Add TypeScript? Yes
✔ Add JSX Support? No
✔ Add Vue Router for Single Page Application development? … No
✔ Add Pinia for state management? … Yes
✔ Add Vitest for Unit Testing? … Yes
✔ Add an End-to-End Testing Solution? › No
✔ Add ESLint for code quality? › Yes
✔ Add Prettier for code formatting? … Yes
```

## Moving files to fix the project structure

```bash
mv src electron
cd vue
mv public/ ../
mv .vscode/ ../
mv src/ ../
mv .gitattributes ../
mv .prettierrc.json ../
```

## Replace everything in 'vite.renderer.config.ts' with the code

```typescript
import { fileURLToPath, URL } from "node:url";

import { defineConfig } from "vite";
import vue from "@vitejs/plugin-vue";
import vueDevTools from "vite-plugin-vue-devtools";

// https://vite.dev/config/
export default defineConfig({
  plugins: [vue(), vueDevTools()],
  resolve: {
    alias: {
      "@": fileURLToPath(new URL("./src", import.meta.url)),
    },
  },
});
```

```typescript
<h1>💖 Hello World!</h1>
<p>Welcome to your Electron application.</p>
```

## Replace the above code in index.html with the following code

```typescript
<div id="app"></div>
```

## And change the 'src' in the following code to electron

```html
<script type="module" src="/src/renderer.ts"></script>
```

```html
<script type="module" src="/electron/renderer.ts"></script>
```

## In 'forge.config.ts' change the path 'src/main.ts' to 'electron/main.ts'

## And change 'src/preload.ts' to 'electron/preload.ts'

## Add to the end of the file electron/renderer.ts

```typescript
import { createApp } from "vue";
import App from "../src/App.vue";

createApp(App).mount("#app");
```

```bash
cd ..

npm install pinia

npm install typescript@latest eslint@latest eslint-plugin-vue@latest @vitest/eslint-plugin@latest @vue/tsconfig@latest @typescript-eslint/eslint-plugin@latest @typescript-eslint/parser@latest @vue/eslint-config-typescript@latest

npm install @tsconfig/node22@latest @types/jsdom@latest @types/node@latest @vue/eslint-config-prettier@latest @vue/test-utils@latest jiti@latest jsdom@latest npm-run-all2@latest prettier@latest vite-plugin-vue-devtools@latest vitest@latest vue-tsc@latest
```

## Integrating tailwind into electron

Install tailwindcss and its peer dependencies, then generate your tailwind.config.js and postcss.config.js files.

```bash
npm install -D tailwindcss@3 postcss autoprefixer

npx tailwindcss init -p
```

## Configure your template paths

Add the paths to all of your template files in your tailwind.config.js file.

### tailwind.config.js

```typescript
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{vue,js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

## Add the Tailwind directives to your CSS

Add the @tailwind directives for each of Tailwind’s layers to your ./src/assets/main.css file.

### main.css

```typescript
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## Import the css in the renderer.ts

```typescript
import '../src/assets/main.css';
```

## Test tailwind

### App.vue

```html
<template>
  <h1 class="text-3xl font-bold underline">
    Hello world!
  </h1>
</template>
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

[tailwindcss with Vite and Vue](https://v3.tailwindcss.com/docs/guides/vite#vue)
