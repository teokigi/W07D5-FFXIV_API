<template lang="html">
  <div class="memberDetail">
      <img class = "MemberImage"v-bind:src="member.Avatar"/>
      <div>
          Rank:  ::<img class="rankicon" v-bind:src="member.RankIcon"/>:: {{member.Rank}}
      </div>
      <div>
        {{member.Name}}

      </div>
      <h2> FF-logs, Fight Data </h2>
      <div class="fflogdatafield" v-if="fflogdata" v-for="fight of fflogdata">
          Encounter:{{fight.encounterName}}, percentile:{{fight.percentile}}, Job Class:{{fight.spec}}, overall rank:{{fight.rank}}
      </div>
      <div lass="fflogdatafield" v-else-if="!fflogdata">
          <img src="../assets/SoD.gif" id="fc_logo"/> Checking fflog for recent fight records.
      </div>
  </div>
</template>

<script>
import {akey} from '../main.js'

export default {

      name:'member-details',
      props:['member'],
      data(){
          return{
              fflogdata: null,
              akey: process.env.VUE_APP_AKEY
          }
      },
      mounted(){
          this.getfflogs()
      },
      methods:{
          getfflogs(){
              fetch(`https://www.fflogs.com:443/v1/parses/character/${this.member.Name}/Zodiark/EU?metric=dps&api_key=${this.akey}`)
              .then(res => res.json())
              .then(resdata => this.fflogdata = resdata)
          }
      }
}
</script>

<style lang="css" scoped>
.MemberImage{
  margin:10px;
  box-shadow:5px 5px 10px red;
}
.rankicon{

}
</style>
