<template>
    <div id="main-container">
      <div id="container-two">
        <div id="name-location">{{ location }}</div>
        <img :src="icon" alt="" id="icon-view">
        <div id="temp-desc" class="values-text">{{ description }}</div>
      </div>
      <div id="container-one">
        <div id="title-temp" class="title-dising">Temperatura actual</div>
        <div id="temp" class="values-text">{{ temperature }} °C</div>
        <div id="title-temp-min" class="title-dising">Min.</div>
        <div id="temp-min" class="values-text">{{ minTemperature }} °C</div>
        <div id="title-temp-max" class="title-dising">Max.</div>
        <div id="temp-max" class="values-text">{{ maxTemperature }} °C</div>
        <div id="title-humidity" class="title-dising">Humedad</div>
        <div id="humidity" class="values-text">{{ humidity }}%</div>
      </div>
      <div id="container-tree">
        <div class="title-dising">Velocidad del viento</div>
        <div id="container-air">
          <div id="speed-air" class="values-text">{{ windSpeed }} m/s</div>
          <img src="../assets/SVG/speedAir.svg" alt="" id="air">
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        location: '',
        icon: '',
        description: '',
        temperature: '',
        minTemperature: '',
        maxTemperature: '',
        humidity: '',
        windSpeed: '',
      };
    },
    mounted() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(position => {
          const lat = position.coords.latitude;
          const lon = position.coords.longitude;
          const key = '0de97a5ffc979248b4a69aa8aabbaf13';
          const url = `https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=${key}&units=metric&lang=es`;
          this.getData(url);
        });
      }
    },
    methods: {
      async getData(url) {
        const response = await axios.get(url);
        const data = response.data;
        this.location = `${data.name} - ${data.sys.country}`;
        this.description = data.weather[0].description;
        this.temperature = Math.floor(data.main.temp);
        this.minTemperature = Math.floor(data.main.temp_min);
        this.maxTemperature = Math.floor(data.main.temp_max);
        this.humidity = data.main.humidity;
        this.windSpeed = data.wind.speed;
        this.insertImgSvg();
      },
      insertImgSvg() {
        const itemIcon = document.getElementById('icon-view');
        const value = this.description;
        switch (value) {
          case 'Thunderstorm':
            itemIcon.src = '/SVG/thunder.svg'; break;
          case 'Drizzle':
            itemIcon.src = '/SVG/rainy-6.svg'; break;
          case 'Rain':
            itemIcon.src = '/SVG/rainy-1.svg'; break;
          case 'Snow':
            itemIcon.src = '/SVG/snowy-1.svg'; break;
          case 'Clear':
            itemIcon.src = '/SVG/day.svg'; break;
          case 'Atmosphere':
            itemIcon.src = '/SVG/cloudy.svg'; break;
          case 'Clouds':
            itemIcon.src = '/SVG/cloudy-day-2.svg'; break;
          default:
            itemIcon.src = '/SVG/cloudy-day-1.svg';
        }
      },
    },
  };
  </script>
  
  <style scoped>
  @import url("../assets/responsive.css");
  
  * {
    margin: 0px;
    padding: 0px;
    font-family: sans-serif;
  }
  
  :root {
    --pad: 10px;
    --colorMain: rgb(254, 254, 254);
    --colorSecond: rgb(220, 220, 220);
    --linerGrad: linear-gradient(135deg, var(--colorMain) 0%, var(--colorSecond) 100%);
  }
  
  body {
    width: 100vw;
    height: 100vh;
    display: grid;
    justify-content: center;
    align-items: center;
  }
  
  #main-container {
    min-width: 80%;
    height: auto;
    padding: 15px;
    grid-gap: 5px;
    border-radius: 10px;
    display: grid;
    grid-template-rows: 40% 40% 20%;
    justify-content: center;
    border: #ccc solid 0.5px;
    text-align: center;
  }
  
  #name-location {
    text-align: center;
    font-weight: 500;
    font-size: 18px;
  }
  
  /*Dising box one*/
  #container-one {
    display: grid;
    padding: 15px;
    width: auto;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: repeat(6, 1fr);
    grid-gap: 5px;
    border-radius: var(--pad);
    background-image: var(--linerGrad);
    animation: fors 2.5s ease infinite alternate;
    background-size: 200% 200%;
  }
  
  #title-temp-min,
  #temp-min {
    grid-column: 1/2;
    border-right: solid 1px #ccc;
  }
  #title-temp,
  #temp {
    grid-column: 1/3;
  }
  #temp {
    border-bottom: solid 1px #ccc;
  }
  #temp-max,
  #title-temp-max {
    grid-column: 2/3;
  }
  #title-temp-max {
    grid-row: 3/4;
  }
  #temp-max {
    grid-row: 4/5;
  }
  #title-humidity,
  #humidity {
    grid-column: 1/3;
  }
  
  #title-humidity {
    border-top: solid 1px #ccc;
    padding-top: 3px;
  }
  
  /*Dising box two*/
  #container-two {
    display: grid;
    padding: 15px;
    width: auto;
    border-radius: var(--pad);
    grid-template-rows: 20% 60% 20%;
    background-image: var(--linerGrad);
    animation: fors 2.5s ease infinite alternate;
    background-size: 200% 200%;
    justify-content: center;
    align-items: center;
  }
  
  #icon-view {
    width: 100%;
  }
  
  /*Dising box two*/
  #container-tree {
    padding: 15px;
    display: grid;
    width: auto;
    border-radius: var(--pad);
    background-image: var(--linerGrad);
    animation: fors 2.5s ease infinite alternate;
    background-size: 200% 200%;
  }
  
  #container-air {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    justify-content: center;
    align-items: center;
  }
  
  #air {
    grid-column: 3/4;
    width: 50%;
  }
  
  #speed-air {
    grid-column: 1/3;
  }
  
  .title-dising {
    font-weight: 500;
    font-size: 16px;
  }
  
  .values-text {
    color: rgb(69, 69, 69);
    font-weight: 200;
    font-size: 15px;
  }
  
  /*Animations*/
  @keyframes fors {
    0% {
      background-position: 0% 2%;
    }
    50% {
      background-position: 50% 55%;
    }
    100% {
      background-position: 100% 99%;
    }
  }
  </style>





