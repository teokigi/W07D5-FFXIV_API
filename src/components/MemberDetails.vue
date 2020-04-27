<template lang="html">
  <div class="memberDetail" :style="{backgroundImage: `url(${getCharacter()})` }">
      <div class="memberHeading">
            <div class="ImageBoxLeft">
            <img class = "MemberImage" v-bind:src="member.Avatar" alt="Avatar"/>
            </div>
            <div>
                    <div>
                        Rank:  ::<img class="rankicon" v-bind:src="member.RankIcon"/>:: {{member.Rank}}
                    </div>
                    <div>
                        {{member.Name}}

                    </div>
                </div>
        </div>
        <div class="fightHeading" v-on:click="toggleView" >FF-Logs</div>
        <div class="fflogdatafield" v-if="logdataview" v-for="fight of member.fflogdata">
            Encounter:{{fight.encounterName}}, percentile:{{Math.round(fight.percentile)}}, Job Class:{{fight.spec}}, overall rank:{{fight.rank}}
        </div>
        <div class="fflogdatafield" v-if="!member.fflogdata">
            <img src="../assets/SoD.gif" id="fc_logo"/> No fflog fight data, click member again to reload
        </div>
  </div>
</template>

<script>
export default {
      name:'member-details',
      data(){
          return{
              logdataview: null
          }
      },
      props:['member'],
      methods:{
          getCharacter(){
              return this.member.Avatar.replace('c0_96x96','l0_640x873')
          },
          toggleView(){
              this.logdataview ? this.logdataview=null : this.logdataview = 'hello'
          }
      }      
}
</script>

<style lang="css" scoped>
.memberDetail{
    height:550px;
    color:white;
    background-color:lightseagreen;
    background-repeat:no-repeat;
    background-size:100%;
    box-shadow: inset 0px 0px 20px white;
    border-radius:30px;
    transform:translateX(0px);
    animation-name:slideright;
    animation-duration:2s;
    padding:20px;
    margin:10px;
    }
@keyframes slideright{
    from{transform:translateX(-800px);}
    to {transform:translateX(0px);}
}
.MemberImage{
    margin:10px;
    box-shadow:5px 5px 10px red;
}
.memberHeading{
    display:flex;
    flex-direction:row;
}
.fightHeading{
    text-align:center;
    width:100px;
    background-color:blue;
    box-shadow:inset 0px 0px 5px white;
    border-radius:50px;
    padding:10px;
}
#fc_logo{
    width:50px;
}
</style>
