<template>
  <div class="body" background-image="./1.jpg" >
    <show :lists="lists" :score-sports="scoreSports" :edit-status="editStatus":add-score-sport="addScoreSport" :delete-event = "deleteEvent":edit-score="editScore" :add-event="addEvent" :add-total-score="addTotalScore"></show>
  </div>
</template>

<script>
import firebase from 'firebase'
var config = {
  apiKey: 'AIzaSyBasyXEYg3xGN6Y9ndOtt9chPV4m60_6Xw',
  authDomain: 'it-3k-1f766.firebaseapp.com',
  databaseURL: 'https://it-3k-1f766.firebaseio.com',
  storageBucket: 'it-3k-1f766.appspot.com',
  messagingSenderId: '914467199924'
}
firebase.initializeApp(config)
var It3k = firebase.database().ref('It3k')
var ScoreSports = firebase.database().ref('ScoreSports')
import Show from './components/Show'
export default {
  components: {
    Show
  },
  data () {
    return {
      lists: [],
      scoreSports: []
    }
  },
  mounted () {
    var vm = this
    It3k.on('child_added', function (snapshot) {
      var item = snapshot.val()
      item.id = snapshot.key
      vm.lists.splice(0, 0, item)
    })
    It3k.on('child_removed', function (snapshot) {
      var id = snapshot.key
      var index = vm.lists.findIndex(lists => lists.id === id)
      vm.lists.splice(index, 1)
    })
    It3k.on('child_changed', function (snapshot) {
      var id = snapshot.key
      var item = snapshot.val()
      if (item.type === 'sport') {
        var sport = vm.lists.find(item => item.id === id)
        sport.type = item.type
        sport.time = item.time
        sport.competition = item.competition
        sport.location = item.location
        sport.status = item.status
        sport.sport = item.sport
        sport.total1 = item.total1
        sport.total2 = item.total2
      }
    })
    ScoreSports.on('child_added', function (snapshot) {
      var item = snapshot.val()
      item.id = snapshot.key
      vm.scoreSports.push(item)
    })
    ScoreSports.on('child_changed', function (snapshot) {
      var id = snapshot.key
      var item = snapshot.val()
      var scoreSport = vm.scoreSports.find(item => item.id === id)
      scoreSport.set = item.set
      scoreSport.sportId = item.sportId
      scoreSport.team1 = item.team1
      scoreSport.team2 = item.team2
      scoreSport.status = item.status
    })
  },
  methods: {
    addEvent (item, oldId) {
      var res = It3k.push(item)
      if (item.type === 'sport') {
        var newScore = {
          set: '1',
          sportId: res.key,
          team1: '0',
          team2: '0',
          status: true
        }
        ScoreSports.push(newScore)
      }
    },
    addScoreSport (key, set, oldId) {
      var newScore = {
        set,
        sportId: key,
        team1: '0',
        team2: '0',
        status: true
      }
      ScoreSports.push(newScore)
      firebase.database().ref('ScoreSports/' + oldId).update({
        status: false
      })
    },
    addTotalScore (id, total1, total2) {
      firebase.database().ref('It3k/' + id).update({
        total1,
        total2
      })
    },
    editScore (team1, team2, id) {
      var vm = this
      firebase.database().ref('ScoreSports/' + id).update({
        team1,
        team2
      })
      vm.status = ''
    },
    editStatus (status, id) {
      firebase.database().ref('It3k/' + id).update({
        status: status
      })
    },
    deleteEvent (id) {
      if (this.lists.find(list => list.id === id && list.type === 'sport')) {
        this.deleteScoreSports(id)
      }
      firebase.database().ref('It3k/' + id).remove()
    },
    deleteScoreSports (id) {
      this.scoreSports.forEach(score => {
        if (score.sportId === id) {
          firebase.database().ref('ScoreSports/' + score.id).remove()
        }
      })
    }
  }
}
</script>
<style lang="css">
@import url('https://fonts.googleapis.com/css?family=PT+Sans');
@import url('https://fonts.googleapis.com/css?family=Kanit|PT+Sans');
body {
  background-color:#fff;
  /*background-image:url('./1.jpg');*/
  /*border-style: solid;*/
  /*border-color:white ;*/
  /*border-width: 5px;*/
  font-family: 'PT Sans', sans-serif;
  font-family: 'Kanit', sans-serif;
  /*font-family: 'Sriracha', cursive;*/
  /*font-size: 10%;*/
}

</style>
