<script setup>
import { ref, onMounted } from 'vue';


import Header from './components/layout/header.vue'
import SearchBar from './components/SearchBar.vue';
import CurrentWeather from './components/weather/CurrentWeather.vue';
import WeatherStatsCard from './components/weather/WeatherStatsCard.vue';
import DailyForecast from './components/weather/DailyForecast.vue';
import Footer from './components/layout/Footer.vue';

// Variables
const theme = ref("dark")

const city = ref(null)
const country = ref(null)
const coordinates = ref({
  lat: null,
  lon:null,
})

const weatherData = ref({
currentTemperature: null ,
apparentTemperature:null,
humidity:null,
precipitation:null,
wind:'' ,
weatherCode:null,
    })

const dailyForecastData = ref({
      date:null,
      minTemps: null,
      maxTemps: null,
      weatherCodes: null,
})
const data = ref(null)
const loading = ref(true)
const errorMessage = ref(null)

const userInpuCityName = ref('')
//functions
const toggleTheme = () =>{
  theme.value = theme.value === "dark" ? "light":"dark"
}

const fetchCity = async () =>{
 try{
    const response = await fetch('http://ip-api.com/json/')

    if(!response.ok){
      throw new Error("Failed to fetch IP location")
    }

    data.value =  await response.json();
    // console.log("City Name",data.value.city)
    // city.value = data.value.city;
    //fetch city coordinates data 

  }
  catch(error){
    console.error(error)
    errorMessage.value = error;
  }
  finally{
    loading.value = false;
  }

  return data.value.city
}

const fetchCityCoordinates = async (cityName) =>{
  loading.value = true;
try{
    const response = await fetch( `https://geocoding-api.open-meteo.com/v1/search?name=${cityName}`)
     
  
    if(!response.ok){
      throw new Error("Failed to fetch IP location")
    }
    const responseData =  await response.json();

    //set country Name
    country.value = responseData.results[0].country;
    // console.log(city.value, country.value)
    
    //fetch city coordinates data 
    return {
    lat:responseData.results[0].latitude,
    lon:responseData.results[0].longitude,
  }
  }
  catch(error){
    console.error(error)
    errorMessage.value = error;
  }
  finally{
    loading.value = false;
  }
}

const fetchWeatherData = async (latitude, longitude) =>{
  // console.log("In Fetch Weather Data", latitude,longitude);
  loading.value = true;
try{
    const response = await fetch(`https://api.open-meteo.com/v1/forecast?latitude=${latitude}&longitude=${longitude}&current=temperature_2m,apparent_temperature,relative_humidity_2m,precipitation,wind_speed_10m,weather_code&timezone=auto&daily=temperature_2m_max,temperature_2m_min,precipitation_sum,wind_speed_10m_max,weather_code&forecast_days=5`)
 
  
    if(!response.ok){
      throw new Error("Failed to fetch IP location")
    }
    const responseData =  await response.json();
    // console.log("Response Data in Fetch Weather",responseData)

    //set daily forecast data
    dailyForecastData.value = {
      date:responseData.daily.time,
      minTemps: responseData.daily.temperature_2m_min,
      maxTemps: responseData.daily.temperature_2m_max,
      weatherCodes: responseData.daily.weather_code
,
    }

    return{
    currentTemperature:responseData.current.temperature_2m ,
    apparentTemperature:responseData.current.apparent_temperature,
    humidity:responseData.current.relative_humidity_2m,
    precipitation:responseData.current.precipitation,
    wind:responseData.current.wind_speed_10m,
    weatherCode:responseData.current.weather_code,
    }
    
    //fetch city coordinates data 
    // return responseData.results[0]
  }
  catch(error){
    console.error(error)
    errorMessage.value = error;
  }
  finally{
    loading.value = false;
  }
}

const handleSubmit = async () =>{
  if (!userInpuCityName.value ) return;

  
  // console.log("In handle Submit")
 city.value = userInpuCityName.value;

 coordinates.value = await fetchCityCoordinates(city.value);
  // console.log("In Mount",cityData)
  // console.log(coordinates)
  // console.log("Coords in mount",coordinates.value.lat, coordinates.value.lon)

  weatherData.value = await fetchWeatherData(coordinates.value.lat, coordinates.value.lon)
  // console.log(weatherData.value)
  // console.log(dailyForecastData.value)

  //clear input
  userInpuCityName.value = "";

}

const reloadPage = async ()=>{

  window.location.reload();

}
onMounted(async (params) => {
 city.value = await fetchCity();

 coordinates.value = await fetchCityCoordinates(city.value);
  // console.log("In Mount",cityData)
  //console.log(coordinates)
  //console.log("Coords in mount",coordinates.value.lat, coordinates.value.lon)

  weatherData.value = await fetchWeatherData(coordinates.value.lat, coordinates.value.lon)
  //console.log(weatherData.value)
 // console.log(dailyForecastData.value)
})



</script>

<template>
  <div id="container">
 <Header  :theme="theme" :toggleTheme="toggleTheme"/>

<main v-if="!errorMessage ">
<h1 class="heading-1 center"> What’s it looking like outside?</h1>

  <SearchBar v-model="userInpuCityName" :onSubmit="handleSubmit"/>

     <article id='content-container'>
   <div class="top-layer">
   <WeatherStatsCard 
   :statsName="'Feels Like'"
    :statsValue="weatherData.apparentTemperature" 
    :unit="'°'" />

    <WeatherStatsCard
    :statsName="'Humidity'"
    :statsValue="weatherData.humidity" 
    :unit="'%'"
    />

    <WeatherStatsCard
    :statsName="'Wind'"
    :statsValue="weatherData.wind" 
    :unit="'km/h'"
    />

    <WeatherStatsCard
    
    :statsName="'Precipitation'"
    :statsValue="weatherData.precipitation" 
    :unit="'mm'"/>
  </div>
   <div class="middle-layer">
    <CurrentWeather 
    :temp="weatherData.currentTemperature"
    :code="weatherData.weatherCode"
    :city="city" 
    :country="country"/>

   </div>
   <div class="bottom-layer">
   <DailyForecast :dates="dailyForecastData.date" :minTemps="dailyForecastData.minTemps" :maxTemps="dailyForecastData.maxTemps" :codes="dailyForecastData.weatherCodes" />
   </div>
  </article>

</main>

<main 
id="error-screen"
v-else-if="errorMessage"
class="flex ">
<h1 class="heading-1 center "> OOPS</h1>
<p>Something went wrong</p>
<p>{{ errorMessage }}</p>
<button @click="reloadPage"> Retry </button>




   
</main>
  </div>
<Footer/>

</template>

