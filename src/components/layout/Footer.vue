<script setup>

</script>


<template>
 <footer className='caption-sm'>
    <div></div>
      <p> &copy; <span className='current-year'>2025</span></p>
      <p className='developer underline'><a href="https://github.com/bee-yy"> Project By Blessing A</a></p>
       
    </footer>
</template>


<style scoped>
footer{
    position: relative;
    background: var(--color-bg-2);
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: var(--spacing-sm) var(--spacing-sm); 
    color: var(--color-text-secondary); 
    margin-top:calc(var(--spacing-xxxl) + 30px) 
}

.open-modal-btn{
    height: 100%;
    all:unset;
}

.developer a{
 color: inherit;
}
.underline{
    text-decoration: underline;
}


dialog {
  position: absolute; 
 background-color: inherit;

  width: 100%;
  height: auto;
  padding: var(--spacing-xxl);
  bottom: 0%;                 
  z-index: 1000; 

  display: flex;
  flex-direction: column;
  gap: var(--spacing-sm);


}

dialog a{
    color: inherit;
}

.close-modal-btn{
    padding: var(--spacing-sm);
    background-color: var(--color-accent);

}
</style>