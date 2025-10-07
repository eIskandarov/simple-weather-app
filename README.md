## 🤸 Demo

Git it a go [here](https://simple-weather-app-tau.vercel.app/) :)

<div align="center">
  <br />
    <a href="#" target="_blank">
      <img src="./src/assets/images/main.png" alt="Vue Weather App">
    </a>
  <br />
  
  <div >
    <img src="https://img.shields.io/badge/Vue.js-4FC08D?style=flat&logo=vue.js&logoColor=white" alt="Vue" />
    <img src="https://img.shields.io/badge/vite-%23646CFF.svg?style=for-the-badge&logo=vite&logoColor=white" alt="Vite  " />
    <img src="https://img.shields.io/badge/JavaScript-323330?style=flat&logo=javascript&logoColor=F7DF1E" alt="javascript" />
  </div>

<h1 align="center">Weather Forecast Mini App</h1> 
</div>

## 📖 About

This is a small Vue-based application that displays a **4-day weather forecast** for a selected city.  
Weather data is fetched from [weatherapi.com](https://www.weatherapi.com/).

## 🛠️ Features & Techniques Used

- **Vue Directives**: `v-on`, `v-bind`, `v-for`, `v-if`, `v-show`, `v-model`
- **Slots**
- **Reactivity & Lifecycle**:
  - `computed` properties
  - `ref` for reactive state
  - Lifecycle hooks: `onMounted`, `onUpdated`
  - `emits` for parent-child communication
- **Custom Directive**: focus directive applied to the city input on mount
- **Dependency Injection**: `provide/inject` usage for sharing state between components

## ⚠️ Known Issues

- Responsivenes is currently NOT supported
- Only the "invalid city" error is currently handled
- Small **CLS (Cumulative Layout Shift)** when selecting a new city
- When focusing the input and pressing **Enter**, the city is immediately applied instead of staying focused
  - (With **Space** the behavior works correctly)
- In the sidebar, the displayed city name is the typed one, not the normalized name returned by the API
