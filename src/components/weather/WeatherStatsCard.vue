<script setup>

</script>


<template>
  <div className="forecast-stats-card">
      <p className='stats-name body-sm'> Stats Name</p>
      <p className='stats-value body-lg'> <span>Value, Unit </span></p>
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