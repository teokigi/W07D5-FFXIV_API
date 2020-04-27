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
      <div class="fflogdatafield" v-if="member.fflogdata.length" v-for="fight of member.fflogdata">
          Encounter:{{fight.encounterName}}, percentile:{{Math.round(fight.percentile)}}, Job Class:{{fight.spec}}, overall rank:{{fight.rank}}
      </div>
      <div class="fflogdatafield" v-if="!member.fflogdata.length">
          <img src="../assets/SoD.gif" id="fc_logo"/> No fflog fight data
      </div>
  </div>
</template>

<script>
export default {
      name:'member-details',
      props:['member'],
}
</script>

<style lang="css" scoped>
.memberDetail{
    color:white;
    background-color:lightseagreen;
    border:solid red;
    border-radius:30px;
    animation-name:slideup;
    animation-duration:10s;
    }
.MemberImage{
  margin:10px;
  box-shadow:5px 5px 10px red;
}
.rankicon{

}
</style>
