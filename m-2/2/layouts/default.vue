<template>
  <div>
    <TheHeader @sidenavToggle="displaySidenav = !displaySidenav"/>
    <TheSideNav :show="displaySidenav" @close="displaySidenav = false"  />
    <nuxt/>
  </div>
</template>

<script>
  import TheHeader from '@/components/Navigation/TheHeader';
  import TheSideNav from '@/components/Navigation/TheSideNav';

  export default {
    middleware: 'log',
    components: {
      TheHeader,
      TheSideNav,
    },
    data(){
      return {
        displaySidenav: false,
      }
    }
  }
</script>


<style>
html{
  font-family: 'Open Sans', sans-serif;
}
body{
  margin:0;
}
</style>
