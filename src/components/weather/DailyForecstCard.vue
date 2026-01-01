<script setup>
import SunnyIcon from "@/assets/images/Sunny.svg"

</script>

<template>
    <div className="daily-forecast-card">
    <p className='day'>Tue</p>
    <div className="icon-container">
      <img :src="SunnyIcon" alt=""/>
    </div>
    <div className='temperature-range'>
      <p> <span> 20 </span> <sup>°</sup> </p>
      <p> <span> 14 </span> <sup>°</sup></p>
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