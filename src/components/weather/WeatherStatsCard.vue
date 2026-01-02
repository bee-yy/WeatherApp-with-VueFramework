<script setup>
const props = defineProps({
  statsName:String,
 statsValue: [Number, String],
  unit:String
   
  
})
</script>


<template>
  <div className="forecast-stats-card">
      <p className='stats-name body-sm'> {{props.statsName}}</p>
      <p className='stats-value body-lg'> <span>{{ Math.round(props.statsValue) }}{{props.unit}} </span></p>
    </div>
</template>


<style scoped>

    .forecast-stats-card{
    background-color: var(--color-bg-2);
    color: var(--color-text-secondary);

    padding: var(--spacing-lg);

    display: flex;
    flex-direction: column;
    gap: var(--spacing-xl);
    border-radius: var(--radius-lg);
}
</style>