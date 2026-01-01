<script setup>
import DailyForecstCard from './DailyForecstCard.vue';
</script>


<template>
    <p className='body-md'>Daily Forecast</p>

    <div className="daily-forecast-cards-container">
       <DailyForecstCard/>
       <DailyForecstCard/>
       <DailyForecstCard/>
       <DailyForecstCard/>
       <DailyForecstCard/>
    </div>
</template>


<style scoped>
.daily-forecast-cards-container{
    /* border: 2px solid red; */
    display: grid;
    grid-template-columns: repeat(3,30%);
    justify-content: center;
    gap: var(--spacing-lg);
}

/*
=====================================
LARGE SCREENS 
=====================================
*/

/* Medium devices (landscape tablets, 768px and up) */
@media only screen and (min-width: 768px){
    .daily-forecast-cards-container{
    

    grid-template-columns: repeat(5,minmax(122px, 1fr));
    
    gap: var(--spacing-md);
}
}

/* Large devices (laptops/desktops, 992px and up) */
@media only screen and (min-width: 992px){}

/* Extra large devices (large laptops and desktops, 1200px and up) */
@media only screen and (min-width: 1200px){}

</style>