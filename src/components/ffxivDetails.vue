<template lang="html">
  <div>
    <h3 class="memberHeading">Members:</h3>
      <MemberList v-for="member of details.FreeCompanyMembers" :item="member" />
  </div>
</template>

<script>
import MemberList from './ItemList.vue'
export default {
  name: 'ffxiv-details',
  props:['details'],
  components:{
    MemberList
  }
}
</script>

<style lang="css" scoped>
.memberHeading{
  font-family:georgia;
  text-decoration-line:underline;
}
</style>
