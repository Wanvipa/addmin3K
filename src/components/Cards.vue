<template lang="html">
  <div class="app">
    <sport-card v-if="list.type==='sport'":list="list" :delete-event = "deleteEvent" :edit-status="editStatus" :score-sports="scoreSports" :add-score-sport="addScoreSport" :edit-score="editScore" :add-total-score="addTotalScore"></sport-card>
    <pic-card v-if="list.type==='Picture'":list="list" :delete-event = "deleteEvent" ></pic-card>
    <program-card v-if="list.type==='Program'":list="list" :delete-event = "deleteEvent" ></program-card>
  </div>
</template>
<script>
import SportCard from './SportCard'
import PicCard from './PicCard'
import ProgramCard from './ProgramCard'
export default {
  props: ['list', 'scoreSports', 'editScore', 'addScoreSport', 'editStatus', 'deleteEvent', 'addTotalScore'],
  data () {
    return {

    }
  },
  computed: {
  },
  mounted () {
  },
  methods: {},
  components: {
    ProgramCard,
    PicCard,
    SportCard
  }
}
</script>

<style lang="css">

.app {
  margin-bottom: 10px;
}
h1{
  color: #d32f2f !important;
  display: inline-block;

}
.width-card {
  width: 100%;
  text-align: center;
  background-color: #fff;
}

.textred{
  color: #d32f2f !important;
  font-size: 60px !important;

}
.texttype{
  color: #009688  !important;
}
.textlocation{
  color: #ef5350  !important;
  font-size: 15px !important;
}
.textstatus{
  color: #42B72A;
  display: inline-block;
}
.sizedate{
  font-size: 13px !important;
  margin-top: auto;
}
small{
  color: black !important;
}

.tap{
  width: 100% ;
  height: 40px;
  padding-top: 3px;
  padding-left: 3px;

}
.iconright
{
  margin-left: 250px;
}

</style>
