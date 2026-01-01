<script setup>
import SunnyIcon from '@/assets/images/Sunny.svg'
</script>

<template>
 <div className='temperature-container'>
    <div className="temperature-icon-container">
      <img width="108" height="108" :src="SunnyIcon" alt=""/>
    </div>
    <p className="temperature display orange">20 <span>°</span></p>
    </div>
    <div className='location-info-container'>
      <p className='location heading-sm orange'>Burnaby,Canada</p>
      <p className='date body-sm fw-normal orange'>January 1, 2026</p>
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