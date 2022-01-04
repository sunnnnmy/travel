<template>
   <transition>
       <slot></slot>
   </transition>
</template>

<script>
    
    import axios from 'axios'
    export default{
        name:"Fade",
      
    }
</script>

<style lang="stylus" scoped>
    .v-enter,.v-leave-to{
        opacity: 0;
    }
    .v-enter-active,.v-leave-active{
        transition: opacity .5s;
    }
</style>