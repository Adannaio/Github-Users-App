<template>
  <div class="navbar">
      <h1>Devfinder</h1>
      <Toggle :mode="mode" @toggle="$emit('toggle')"/>
  </div>  
</template>

<script>
import Toggle from '@/components/Toggle.vue'
export default{
  props: ['mode'],
  components : {
    Toggle
  }
}
</script>

