<template lang="html">
<div class="">
  <div  class ="width-card"v-show="list.type==='sport'">
    <div class="card-content">
      <div class="media">
        <div class="media-content">
            <p class="title is-5 ">
              <i class="fa fa-futbol-o " aria-hidden="true"></i>
              &nbsp;{{list.sport}} ( {{list.status}} )<br>
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<small>{{timeout}}</small>
              <button @click="editsta">on</button>
              <button @click="deleteEvent">X</button>
            </p>
          </div>
      </div>
      <div class="content"><br>
        <h5 class="subtitle is-5 ">{{list.competition}}</h5>
        <div class="" v-for="score in scoreSports" v-show="score.sportId === list.id && score.status">SET {{score.set}} ( {{list.kind}} )
          <h2 class="title is-2 textred ">{{score.team1}} - {{score.team2}}</h2>
          ( {{list.total1}} - {{list.total2}} )<br><br>
          <h5 class="subtitle is-6 ">location : {{list.location}}<br><br>
            <small class="sizedate">{{list.time}}</small>
          </div>
        </div>
      </div>
            <a class="button is-primary" @click="addSet">Add Set</a><br><br> SET 1 :
            <a class="button is-primary" @click="reduceScoreTeam1">-</a>
            <a class="button is-primary" @click="addScoreTeam1">+</a> SET 2 :
            <a class="button is-primary" @click="reduceScoreTeam2">-</a>
            <a class="button is-primary" @click="addScoreTeam2">+</a><br>

      </div>
    </div>




</template>

<script>
export default {
  props: ['list', 'scoreSports', 'editScore', 'addScoreSport', 'editStatus', 'deleteEvent', 'addTotalScore'],
  data () {
    return {}
  },
  computed: {
    timeout () {
      var time = ''
      if (this.list.timePost) {
        var timePost = this.list.timePost.split(':')
        var timeAgo = parseInt(timePost[0]) * 60 + parseInt(timePost[1])
        var today = new Date()
        var timeNow = today.getHours() * 60 + today.getMinutes()
        if (timeAgo === timeNow) {
          time = 'เมื่อสักครู่นี้'
        } else {
          if (timeNow - timeAgo < 60) {
            time = (timeNow - timeAgo) + 'นาทีที่แล้ว'
          } else {
            time = (parseInt(timeNow / 60) - parseInt(timeAgo / 60)) + 'ชั่วโมงที่แล้ว'
          }
        }
      }
      return time
    }
  },
  mounted () {},
  methods: {
    addSet () {
      var vm = this
      let score = this.scoreSports.find(score => score.sportId === vm.list.id && score.status)
      this.addScoreSport(this.list.id, parseInt(score.set) + 1, score.id)
      let total1 = this.list.total1
      let total2 = this.list.total2
      if (score.team2 < score.team1) {
        total1 = this.list.total1 + 1
      }
      if (score.team2 > score.team1) {
        total2 = this.list.total2 + 1
      }
      this.addTotalScore(this.list.id, total1, total2)
    },
    addScoreTeam1 () {
      var vm = this
      var score = this.scoreSports.find(score => score.sportId === vm.list.id && score.status)
      this.editScore(parseInt(score.team1) + 1, score.team2, score.id)
    },
    addScoreTeam2 () {
      var vm = this
      var score = this.scoreSports.find(score => score.sportId === vm.list.id && score.status)
      this.editScore(score.team1, parseInt(score.team2) + 1, score.id)
    },
    reduceScoreTeam1 () {
      var vm = this
      var score = this.scoreSports.find(score => score.sportId === vm.list.id && score.status)
      this.editScore(parseInt(score.team1) - 1, score.team2, score.id)
    },
    reduceScoreTeam2 () {
      var vm = this
      var score = this.scoreSports.find(score => score.sportId === vm.list.id && score.status)
      this.editScore(score.team1, parseInt(score.team2) - 1, score.id)
    },
    editsta () {
      var status
      if (this.list.status === 'จบการแข่งขัน') {
        status = 'กำลังแข่งขันอยู่'
      } else {
        status = 'จบการแข่งขัน'
      }
      this.editStatus(status, this.list.id)
    }
  },
  components: {
  }
}
</script>

<style lang="css">

</style>
