<template lang="html">
  <div>
      <div id="header">
        <span class="tital" @click="home">
          <i class="fa fa-home"></i>
        </span>
        <span class="tital" @click="inputData = !inputData">
          <i class="fa fa-keyboard-o" aria-hidden="true"></i>
        </span>
      </div>
        <div class="column">
         <!-- <h6 class="subtitle is-6">{{user.displayName}}</h6> -->
        </div>
        <div class="column" v-if="!inputData"><br><br>
          ชื่อผู้เข้าใช้ : <h1>{{user.displayName}}</h1>
          <span  @click="signOut">
            <i class="fa fa-sign-out icon is-medium" style="color: black;"></i>
          </span>
          <cards :list="list" :delete-event = "deleteEvent" :edit-status="editStatus" :score-sports="scoreSports" :add-score-sport="addScoreSport" :edit-score="editScore" v-for="list in lists" :add-total-score="addTotalScore"></cards>
        </div>
        <div class="column" v-if="inputData">
          <fromInput :user="user" :add-event="addEvent"></fromInput>
        </div>
  </div>

</template>
<script>
import Cards from './Cards'
import fromInput from './Add'
export default {
  props: ['user', 'signOut', 'lists', 'addEvent', 'scoreSports', 'editScore', 'addScoreSport', 'editStatus', 'deleteEvent', 'addTotalScore'],
  data () {
    return {
      inputData: false
    }
  },
  computed: {},
  mounted () {},
  methods: {
    home () {
      window.scrollTo(0, 0)
    }
  },
  components: {
    Cards,
    fromInput
  }
}
</script>

<style lang="css">
h6{
  margin-top: -50px;
  font-size: 1.3em !important;
  text-align: center;
  padding-left: 35px;
  width: 100%;
  color: white !important;
}
h3 {
  text-align: center;
  margin-top: 0px;
}
.tital{
  color: #fff;
  font-size: 40px;
  /*text-align: center;*/
}
.tap{
  width: 100%;
}
#header {
  position: fixed;
  width: 100%;
  margin-left: 0%;
  margin-right: 0%;
  height: 60px;
  display: inline-block;
  background:#ef5350 ;
  padding: 10px;
  font-variant: small-caps;
  font-weight: bold;
  color: #fff;
  box-shadow: 0 0 5px #000;
  z-index: 999;
}
.buttdel{
  background-color: red !important;
}
.tapstatus{
  margin-left: -15px;
}
.buttonoff{
background-color: green !important;
}
</style>
