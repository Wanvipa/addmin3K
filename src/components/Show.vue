<template lang="html">
  <div>
      <div id="header">
        <span class="tital" @click="home">
          <i class="fa fa-home"></i>
        </span>
        <span class="tital" @click="inputData = !inputData">
          <i class="fa fa-keyboard-o" aria-hidden="true"></i></span>
          <h6 class="subtitle is-6">IT3K-13th (admin)</h6>
        </div>
        <div class="column">

        </div>
        <div class="column" v-show="!inputData"><br><br>
          <cards :list="list" :delete-event = "deleteEvent" :edit-status="editStatus" :score-sports="scoreSports" :add-score-sport="addScoreSport" :edit-score="editScore" v-for="list in lists" :add-total-score="addTotalScore"></cards>
        </div>
        <div class="column" v-show="inputData">
          <fromInput :add-event="addEvent"></fromInput>
        </div>


  </div>

</template>
<script>
import Cards from './Cards'
import fromInput from './Add'
export default {
  props: ['lists', 'addEvent', 'scoreSports', 'editScore', 'addScoreSport', 'editStatus', 'deleteEvent', 'addTotalScore'],
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
  margin-top: -45px;
  font-size: 1.5em !important;
  text-align: center;
  padding-left: 60px;
  width: 100%;
  color: white !important;
}
.tital{
  color: #fff;
  font-size: 40px;
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


</style>
