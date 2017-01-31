<template lang="html">
<div class="">
  <div  class ="width-card" v-show="list.sport === 'Badminton' || list.sport === 'Table Tennis' ||  list.sport === 'Volleyball'">
    <div class="card-content">
      <div class="media">
        <div class="media-content">
            <p class="title is-5 ">
              <img src="./sport.png" alt=""> {{list.sport}} ( {{list.status}} )<br>
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<small>{{fromNow}}</small>
              <a class="button is-primary buttonoff"  @click="editsta">ON</a>
              <a class="button is-primary buttdel"  @click="deleteEvent(list.id)">ลบ</a>
            </p>
          </div>
        </div>
        <div class="content"><br>
          <h5 class="subtitle is-5 ">{{list.competition}}</h5>
          <div class="" v-for="score in scoreSports" v-show="score.sportId === list.id && score.status">SET {{score.set}} {{list.kind}}
            <h2 class="title is-2 textred ">{{score.team1}} - {{score.team2}}</h2>
            ( {{list.total1}} - {{list.total2}} )<br><br>
            <a :href="list.locationLink"><h5 class="subtitle is-5 textlocation"><i class="fa fa-map-marker location" aria-hidden="true"></i> : {{list.location}}</a>
            Admin: {{list.admin}}
          </div>
        </div>
      </div>
      <a class="button is-primary" @click="addSet">Add Set</a><br><br> team 1 :
      <a class="button is-primary" @click="reduceScoreTeam1" :disabled="scoreTeam(1)">-</a>
      <a class="button is-primary" @click="addScoreTeam1">+</a> team 2 :
      <a class="button is-primary" @click="reduceScoreTeam2" :disabled="scoreTeam(2)">-</a>
      <a class="button is-primary" @click="addScoreTeam2">+</a><br><br>
    </div>
    <div v-show="list.sport === 'Basketball'" class ="width-card">
      <div class="card-content">
        <div class="media">
          <div class="media-content">
              <p class="title is-5 ">
                <img src="./sport.png" alt=""> {{list.sport}} ( {{list.status}} )<br>
                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<small>{{fromNow}}</small>
                <a class="button is-primary buttonoff"  @click="editsta">ON</a>
                <a class="button is-primary buttdel"  @click="deleteEvent(list.id)">ลบ</a>
              </p>
            </div>
          </div>
          <div class="content"><br>
            <h5 class="subtitle is-5 ">{{list.competition}}</h5>
            <div class="" v-for="score in scoreSports" v-show="score.sportId === list.id && score.status">ประเภท : {{list.kind}}
              <h2 class="title is-2 textred ">{{score.team1}} - {{score.team2}}</h2>
              ( {{list.total1}} - {{list.total2}} )<br><br>
              <a :href="list.locationLink"><h5 class="subtitle is-5 textlocation"><i class="fa fa-map-marker location" aria-hidden="true"></i> : {{list.location}}</a>
              Admin: {{list.admin}}
            </div>
          </div>
        </div>
        <a class="button is-primary" @click="addSet">Add Set</a><br><br> team 1 :
        <a class="button is-primary" @click="reduceScoreTeam1" :disabled="scoreTeam(1)">-</a>
        <a class="button is-primary" @click="addScoreTeam1">+</a> team 2 :
        <a class="button is-primary" @click="reduceScoreTeam2" :disabled="scoreTeam(2)">-</a>
        <a class="button is-primary" @click="addScoreTeam2">+</a><br><br>
      </div>
      <div v-show="list.sport === 'Football'"  class ="width-card">
        <div class="card-content">
          <div class="media">
            <div class="media-content">
                <p class="title is-5 ">
                  <img src="./sport.png" alt=""> {{list.sport}} ( {{list.status}} )<br>
                  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<small>{{fromNow}}</small>
                  <a class="button is-primary buttonoff"  @click="editsta">ON</a>
                  <a class="button is-primary buttdel"  @click="deleteEvent(list.id)">ลบ</a>
                </p>
              </div>
            </div>
            <div class="content"><br>
              <h5 class="subtitle is-5 ">{{list.competition}}</h5>
              <div class="" v-for="score in scoreSports" v-show="score.sportId === list.id && score.status">
                <h2 class="title is-2 textred ">{{score.team1}} - {{score.team2}}</h2>
                <a :href="list.locationLink"><h5 class="subtitle is-5 textlocation"><i class="fa fa-map-marker location" aria-hidden="true"></i> : {{list.location}}</a>
                Admin: {{list.admin}}
              </div>
            </div>
          </div>team 1 :
          <a class="button is-primary" @click="reduceScoreTeam1" :disabled="scoreTeam(1)">-</a>
          <a class="button is-primary" @click="addScoreTeam1">+</a> team 2 :
          <a class="button is-primary" @click="reduceScoreTeam2" :disabled="scoreTeam(2)">-</a>
          <a class="button is-primary" @click="addScoreTeam2">+</a><br><br>
        </div>
  </div>
</template>

<script>
/* global moment */
export default {
  props: ['list', 'scoreSports', 'editScore', 'addScoreSport', 'editStatus', 'deleteEvent', 'addTotalScore'],
  data () {
    return {
      timestamp: '',
      count: 0
    }
  },
  created () {
    let vm = this
    setInterval(() => {
      vm.count++
    }, 1000)
  },
  computed: {
    fromNow () {
      this.count
      this.timestamp = moment(this.list.time)
      return moment(this.timestamp).fromNow()
    }
  },
  mounted () {
    moment.lang('th')
  },
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
      if (score.team1 > 0) this.editScore(parseInt(score.team1) - 1, score.team2, score.id)
    },
    reduceScoreTeam2 () {
      var vm = this
      var score = this.scoreSports.find(score => score.sportId === vm.list.id && score.status)
      if (score.team2 > 0) this.editScore(score.team1, parseInt(score.team2) - 1, score.id)
    },
    editsta () {
      var status
      if (this.list.status === 'จบการแข่งขัน') {
        status = 'กำลังแข่งขันอยู่'
      } else {
        status = 'จบการแข่งขัน'
      }
      this.editStatus(status, this.list.id)
    },
    scoreTeam (team) {
      var vm = this
      var score = this.scoreSports.find(score => score.sportId === vm.list.id && score.status)
      if (score) {
        if (team === 1) {
          return score.team1 <= 0
        } else if (team === 2) {
          return score.team2 <= 0
        }
      }
    }
  },
  components: {
  }
}
</script>

<style lang="css">

</style>
