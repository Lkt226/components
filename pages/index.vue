<template>
  <div id="body">
      <component v-for="(value, index) in size" :key="index"
          :is="'c'+index" class="grid-area" :style="`--i: ${index};`"/>
  </div>
</template>

<script>
export default {
  computed:{
    component_controller(){
      return ['c0', 'c1']
    }
  },
  data(){
    return {
      size: false
    }
  },
  async fetch(){
    let counter = 0;

    while (true) {
      try {
        const check = (await import('@/projects/c'+counter))
        counter++;  

      } catch (error) {
        console.log('acabou em '+counter)
        break;
      }
    }

    this.size = counter;
  }
}
</script>


<style lang="scss" scoped>
  #body{
    @apply grid grid-flow-col-dense 
            auto-cols-max auto-rows-min
            gap-2 p-12;

    .grid-area{
      @apply bg-light-600 p-6 shadow-lg relative;
      &::before{
        counter-reset: i var(--i);
        content: counter(i);

        @apply absolute left-2 top-0;
      }
    }
  }
</style>