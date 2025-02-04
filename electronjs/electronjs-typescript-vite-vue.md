# Setting up Electron + TypeScript + Vite + Vue

## Creating the Electron project

```bash
npx create-electron-app@latest {project_name} --template=vite-typescript
cd {project_name}
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

## Starting the app

```bash
npm start
```

## Documentation

[Electron Forge + Vite Template](https://www.electronforge.io/templates/vite-+-typescript)

[Electron Forge Framework Integration with Vue 3](https://www.electronforge.io/guides/framework-integration/vue-3)

[Electron Forge Plugin Vite](https://www.electronforge.io/config/plugins/vite)

[Vue 3 Quick Start Guide](https://vuejs.org/guide/quick-start.html)