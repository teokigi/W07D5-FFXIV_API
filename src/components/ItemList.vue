<template lang="html">
  <div class="member">
    <img v-bind:src="item.Avatar" v-on:click="clickHandle"/>
    <span class="tooltip"><img v-bind:src="item.RankIcon"/>{{item.Name}}</span>
  </div>
</template>

<script>
import {eventBus} from '../main.js'
import {akey} from '../main.js'

export default {
  name: 'item-list',
  props:['item'],
  // data(){
  //   return{
  //     akey: process.env.VUE_APP_AKEY
  //   }
  // },
  methods:{
    clickHandle(){
      if (!this.item['fflogdata']){
      fetch(`https://www.fflogs.com:443/v1/parses/character/${this.item.Name}/Zodiark/EU?metric=dps&api_key=${process.env.VUE_APP_AKEY}`)
      .then(res => res.json())
      .then(resdata => this.item['fflogdata'] = resdata)
      .then(eventBus.$emit('clickedMember', this.item))
      }
    }
  }
}
</script>

<style lang="css" scoped>
.tooltip{
  visibility:hidden;
  width:200px;
  background-color:black;
  color:#fff;
  text-align:center;
  padding:5px 0;
  border-radius: 10px;
  position:fixed;
  top:50px;
  left:5px;
  z-index:1;
}
.member:hover .tooltip {
  visibility:visible;
}
</style>
