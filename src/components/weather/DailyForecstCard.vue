<script setup>
import SunnyIcon from "@/assets/images/Sunny.svg"
import weatherCodeMap from "./weatherCodes";

const props =defineProps({
  date:String,
  minTemp:Number,
  maxTemp:Number,
  code:Number
})


 function getDate(dateInput){
  //Thursday, Dec 5, 2025
  let date = new Date(dateInput);
  return date.toLocaleDateString('en-US', { 
      weekday: 'short',
    });}
</script>

<template>
    <div class="daily-forecast-card">
    <p class='day'>{{ getDate(props.date)}}</p>
    <div class="icon-container">
      <img :src="weatherCodeMap[code]" :lt="weatherCodeMap[code]"/>
    </div>
    <div class='temperature-range'>
      <p> <span> {{Math.round(props.minTemp)}} </span> <sup>°</sup> </p>
      <p> <span> {{Math.round(props.maxTemp)}}</span> <sup>°</sup></p>
    </div>
    </div>
</template>

<style scoped>
.daily-forecast-card{
background-color: var(--color-bg-2);
border-radius: var(--radius-lg);
color: var(--color-text-secondary);

display: flex;
flex-direction: column;
justify-content: center;
align-items: center;

padding: var(--spacing-md) var(--spacing-md);
}

.temperature-range{
    /* border: 2px solid; */
    width: 100%;
    display: flex;
    justify-content: space-between;

    
}
</style>