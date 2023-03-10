# quarn-app

This template should help get you started developing with Vue 3 in Vite.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur) + [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin).

## Customize configuration

See [Vite Configuration Reference](https://vitejs.dev/config/).

## Project Setup

```sh
yarn
```

### Vue Audio Visual Plugin

```sh
npm install --save vue-audio-visual
```

### Use Audio plugin

Install plugin in main.js:

```sh
import { createApp } from 'vue'
import App from './App.vue'
import { AVPlugin } from 'vue-audio-visual'

const app = createApp(App)
app.use(AVPlugin)

app.mount('#app')
```
Know More Audio Plugin [Click here](https://www.npmjs.com/package/vue-audio-visual#install)

### Compile and Hot-Reload for Development

```sh
yarn dev
```

### Compile and Minify for Production

```sh
yarn build
```
Demo Link : [Click here](https://quran-app-creativehabibur.vercel.app/)
