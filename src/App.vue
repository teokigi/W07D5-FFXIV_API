<template lang="html">
  <body id="app">
    <h1>Hello Eorzea</h1>
    <div class="PaneBody">
        <div class="leftPane">
          
        </div>
        <div class="mainPane">

        </div>
  </div>
  </body>
</template>

<script>
export default {
  name:'App',
  data(){
    return{
      ffxivapi: null
    }
  },
  mounted(){
    this.getffxivapi()
  },
  methods:{
    getffxivapi(){
      console.log('')
      fetch("https://staging.xivapi.com/freecompany/9229283011365729585?data=FCM")
    .then(res => res.json())
    .then(resstuff => this.ffxivapi=resstuff)
    }
  }
}
</script>

<style lang="css" scoped>
body{
  width:100%;
  height:100%;
  overflow:hidden;
  margin:0px;
  padding:5px;

  border:solid blue;
  border-width:thin;
  box-sizing:border-box;

  display:block;
  text-align:center;
  align-items:center;
  }
div{
  border:solid red;
  border-width:thin;
}
</style>
<!-- MVP
The application should display data from an API request.
The application should have a clear separation of concerns (multiple components)
Take input from the user to update the page. You could update the page by filtering or manipulating the data on user interaction, or you might make further API requests to load more data that is then displayed.
Extensions
Looking into a library to visual the data.

Leaflet is an open-source library for rendering maps
Google Charts is a library for rendering charts and graphs
Canvas is a drawing surface for JavaScript.
You will need to use the library’s documentation to integrate it into your application. -->
