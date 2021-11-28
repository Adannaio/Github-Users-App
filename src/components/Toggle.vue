<template>
   <div class="toggle-wrapper">
        <label class="toggle">
            <input type="checkbox"  @change="$emit('toggle')"/>
            <span class="toggler round"></span>
        </label>  
      </div>
</template>

<script>
export default {

}
</script>

