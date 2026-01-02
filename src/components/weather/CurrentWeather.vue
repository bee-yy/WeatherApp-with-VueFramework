<script setup>
import SunnyIcon from '@/assets/images/Sunny.svg'
import weatherCodeMap from './weatherCodes';

const props = defineProps({
temp:Number,
code:Number,
city:String,
country:String,
})

  function getDate(){
  //Thursday, Dec 5, 2025
  let date = new Date();
  return date.toLocaleDateString('en-US', { 
      weekday: 'long', 
      month: 'short', 
      day: 'numeric', 
      year: 'numeric' 
    });}
</script>

<template>
 <div class='temperature-container'>
    <div class="temperature-icon-container">
      <img width="108" height="108" :src="weatherCodeMap[code]" alt=""/>
    </div>
    <p class="temperature display orange">{{Math.round(props.temp)}} <span>°</span></p>
    </div>
    <div class='location-info-container'>
      <p class='location heading-sm orange'>{{city}}, {{country}}</p>
      <p class='date body-sm fw-normal orange '>{{getDate()}}</p>
      </div> 
    
</template>


<style scoped>
.temperature-container{
/* border: 2px solid green; */
display: flex;
gap: var(--spacing-lg);
align-items: center;
justify-content: center;
}

.location-info-container{
/* border: 2px solid red; */
display: flex;
flex-direction: column;
justify-content: center;
align-items: center;
gap: var(--spacing-md);
}
</style>