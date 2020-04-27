<template lang="html">
  <body id="app">
      <div class="TopPane">
          <h1>Final Fantasy XIV: Free Company, Souls Of Dragons</h1>
      </div>
      <div class="MidPane">
          <div class="MidPaneLeft">
              <ffxivDetails v-if="ffxivapi" :details="ffxivapi" />
              <div v-if="!ffxivapi">
                  <img src="./assets/SoD.gif" class="fc_logo"/><hr><hr>
                  Loading Members, please hold yer chocobos
              </div>
          </div>
          <div class="MidPaneBody">
            <MemberDetails :member="selected" v-if="selected"/>
              <div v-if="!selected">
                  click on a member on the left to view his or her details
              </div>
          </div>
      </div>
  </body>
</template>

<script>
import ffxivDetails from './components/ffxivDetails.vue'
import MemberDetails from './components/MemberDetails.vue'
import {eventBus} from './main.js'

export default {
  name:'App',
  data(){
    return{
      ffxivapi: null,
      selected: null,
    }
  },
  mounted(){
    this.getffxivapi()

    eventBus.$on('clickedMember',member => {
      return this.selected = member})
  },
  methods:{
    getffxivapi(){
      fetch("https://staging.xivapi.com/freecompany/9229283011365729585?data=FCM")
    .then(res => res.json())
    .then(resstuff => this.ffxivapi=resstuff)

    }
  },
  components:{
    ffxivDetails,
    MemberDetails
  }
}
</script>

<style lang="css" scoped>
#app{
  width:100%;
  height:100%;
  margin:0px;
  padding:0px;
  background-color:black;
  border-width:thin;
  display:flex;
  flex-direction:column;
  }
.fc_logo{
  width:75px;
}
.TopPane{
  width:100%;
  height:100px;
  text-align:center;
  color:#0055FF;
  font-family:georgia;
  font-size:16px;
  text-shadow:2px 1px 5px white;
  box-shadow: inset 0px 0px 10px black;
  border: solid 5px;
  box-sizing:border-box;
  border-radius:50px;
  background-color:#220022;
}
.MidPane{
  width:100%;
  height:800px;
  display:flex;
  flex-direction:row;
  overflow-y:scroll;
}
.MidPaneLeft{
  width:150px;
  height:700px;
  overflow-y:scroll;
  text-align:center;
  
  background-color:lightblue;
  border: solid white;
  border-radius:50px;
}
.MidPaneLeft::-webkit-scrollbar { 
      display:none;
      }
.MidPaneBody{
  width:700px;
  height:700px;
}
</style>
<!-- MVP
done - The application should display data from an API request.
done - The application should have a clear separation of concerns (multiple components)
todo - Take input from the user to update the page. You could update the page by filtering or manipulating the data on user interaction, or you might make further API requests to load more data that is then displayed.
Extensions
todo - Looking into a library to visual the data.

Leaflet is an open-source library for rendering maps
Google Charts is a library for rendering charts and graphs
Canvas is a drawing surface for JavaScript.
You will need to use the library’s documentation to integrate it into your application. -->
