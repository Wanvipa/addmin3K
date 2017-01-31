<template>
  <div class="body" background-image="./1.jpg" >
    <show v-show="isAdmin" :user="user" :sign-out="signOut" :lists="lists" :score-sports="scoreSports" :edit-status="editStatus":add-score-sport="addScoreSport" :delete-event = "deleteEvent":edit-score="editScore" :add-event="addEvent" :add-total-score="addTotalScore"></show>
    <div v-show="!isAdmin">
      <h1>Welcome to Admin IT3K App</h1>
      <div v-show="!user.uid" >
        <div id="firebaseui-auth-container"></div>
      </div>
      <div v-show="user.uid">
        <h1>{{user.email}}</h1><br>
        <h1>You is not Admin plase sign out</h1><br>
        <button type="button" @click="signOut" name="button">signOut</button>
      </div>
    </div>
  </div>
</template>

<script>
import firebase from 'firebase'
import firebaseui from 'firebaseui'
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
var Admins = firebase.database().ref('Admins')
// var provider = new firebase.auth.GoogleAuthProvider()
// provider.addScope('https://www.googleapis.com/auth/plus.login')
var uiConfig = {
  signInSuccessUrl: '/',
  signInOptions: [
    // Leave the lines as is for the providers you want to offer your users.
    firebase.auth.GoogleAuthProvider.PROVIDER_ID
  ],
  // Terms of service url.
  tosUrl: 'adminit3k.firebaseapp.com'
}

// Initialize the FirebaseUI Widget using Firebase.
var ui = new firebaseui.auth.AuthUI(firebase.auth())
// The start method will wait until the DOM is loaded.
ui.start('#firebaseui-auth-container', uiConfig)
import Show from './components/Show'
export default {
  components: {
    Show
  },
  data () {
    return {
      lists: [],
      scoreSports: [],
      user: '',
      admins: []
    }
  },
  computed: {
    isAdmin () {
      var vm = this
      if (this.user !== '') {
        var check = vm.admins.find(admin => admin.uid === this.user.uid)
        if (check) {
          return true
        } else return false
      } else return false
    }
  },
  mounted () {
    this.initApp()
    var vm = this
    Admins.on('child_added', function (snapshot) {
      var item = snapshot.val()
      item.id = snapshot.key
      vm.admins.splice(0, 0, item)
    })
    Admins.on('child_removed', function (snapshot) {
      var id = snapshot.key
      var index = vm.admins.findIndex(admin => admin.id === id)
      vm.admins.splice(index, 1)
    })
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
        sport.kind = item.kind
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
    ScoreSports.on('child_removed', function (snapshot) {
      var id = snapshot.key
      var index = vm.scoreSports.findIndex(scoreSport => scoreSport.id === id)
      vm.scoreSports.splice(index, 1)
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
    },
    initApp () {
      var vm = this
      firebase.auth().onAuthStateChanged(function (user) {
        if (user) {
            // User is signed in.
          // var displayName = user.displayName
          // var email = user.email
          // var emailVerified = user.emailVerified
          // var photoURL = user.photoURL
          // var uid = user.uid
          // var providerData = user.providerData
          vm.user = user
          user.getToken().then(function (accessToken) {
            // document.getElementById('sign-in-status').textContent = 'Signed in'
            // document.getElementById('sign-in').textContent = 'Sign out'
            // document.getElementById('account-details').textContent = JSON.stringify({
            //   displayName: displayName,
            //   email: email,
            //   emailVerified: emailVerified,
            //   photoURL: photoURL,
            //   uid: uid,
            //   accessToken: accessToken,
            //   providerData: providerData
            // }, null, '  ')
          })
        } else {
            // User is signed out.
          // document.getElementById('sign-in-status').textContent = 'Signed out'
          // document.getElementById('sign-in').textContent = 'Sign in'
          // document.getElementById('account-details').textContent = 'null'
        }
      }, function (error) {
        console.log(error)
      })
    },
    signOut () {
      firebase.auth().signOut()
      this.user = ''
      window.location.assign('https://accounts.google.com/Logout?hl=th&continue=https://www.google.com')
      // window.location.replace('https://admin3k-725fd.firebaseapp.com')
    }
  }
}
</script>
<style lang="css">
@import url('https://fonts.googleapis.com/css?family=PT+Sans');
@import url('https://fonts.googleapis.com/css?family=Kanit|PT+Sans');
body {
  background-color:#fff !important;
  height: 100vh ;
  font-family: 'PT Sans', sans-serif;
  font-family: 'Kanit', sans-serif;
}


</style>
