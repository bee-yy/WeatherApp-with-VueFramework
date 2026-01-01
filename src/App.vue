<script setup>

import Header from './components/layout/header.vue'
import SearchBar from './components/SearchBar.vue';
import CurrentWeather from './components/weather/CurrentWeather.vue';
import WeatherStatsCard from './components/weather/WeatherStatsCard.vue';
import DailyForecast from './components/weather/DailyForecast.vue';

</script>

<template>
  <div id="container">
 <Header />

<main>
<h1 class="heading-1 center"> What’s it looking like outside?</h1>

  <SearchBar/>

    
     <article id='content-container'>
   <div className="top-layer">
   <WeatherStatsCard/>
    <WeatherStatsCard/>
    <WeatherStatsCard/>
    <WeatherStatsCard/>
  </div>
   <div className="middle-layer">
    <CurrentWeather />

   </div>
   <div className="bottom-layer">
   <DailyForecast />
   </div>
  </article>



</main>
  </div>

</template>

