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
  margin-bottom: 20px;
}


.width-card {
  width: 100%;
  margin-left: 0%;
  margin-right: 0%;
  text-align: center;
  color: pink;
  background-color: #FFFFFF ;
  border-top:1px solid #EFEFEF;
  /*border-radius: 5px;*/
  /*box-shadow: 0px 2px 5px #888888;*/
}
.text{
  color: white;
}
.textblack{
  color: black;
}
.textstatus{
  color: #42B72A;
}
.sizefont{
  font-size: 17px;
}
.headericon{
  padding-right:70px;
}

.tapicon{
  padding-right: 90px;
}
.tapsport{
  width: 100%;
  background-color:#EFEFEF ;
  height: 30px;
  border-radius: 9px;
  padding-top: 5px;
  padding-left: 5px;
  color: gray;
}

.tapprogram{
  width: 100%;
  background-color:#EFEFEF ;
  height: 30px;
  border-radius: 9px;
  padding-top: 5px;
  padding-left: 5px;
}

.tappic{
  width: 100%;
  background-color:#EFEFEF;
  height: 30px;
  border-radius: 9px;
  padding-top: 5px;
  padding-left: 5px;

}
</style>
