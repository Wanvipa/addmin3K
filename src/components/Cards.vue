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
.app{
  margin-top:40px !important;
}
.width-card {
  width: 100%;
  text-align: center;
  background-color: pink;
  border-top:1px solid #EFEFEF;
  border-color: #ccff90;
}

.textred{
  color: #d32f2f !important;
}
.textstatus{
  color: #42B72A;
}
.sizedate{
  font-size: 13px !important;
  margin-top: auto;
}

</style>
