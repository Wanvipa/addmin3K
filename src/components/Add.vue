<template lang="html">
  <div class="add">
    <center>
    <a class="button is-primary is-outlined" @click="mode ='sport'" >Sport</a>
    <a class="button is-primary is-outlined" @click="mode ='picture'" >Picture</a>
    <a class="button is-primary is-outlined" @click="mode ='event'" >Program</a>
  </center>
    <add-program v-show="mode === 'event'" :add-event="addEvent"> </add-program>
    <add-sport v-show="mode === 'sport'" :add-event="addEvent"> </add-sport>
    <add-pic v-show="mode === 'picture'" :add-event="addEvent"> </add-pic>
    </div>
</template>

<script>
import AddPic from './AddPic'
import AddProgram from './AddProgram'
import AddSport from './AddSport'
export default {
  props: ['addEvent'],
  data () {
    return {
      type: '',
      time: '',
      picture: '',
      caption: '',
      mode: 'sport'
    }
  },
  computed: {},
  mounted () {},
  methods: {
  },
  components: {
    AddPic,
    AddProgram,
    AddSport
  }
}
</script>

<style lang="css">
.add{
  margin-top: 50px;
  background-color: white;
  width: 100%;
  height: 100vh ;
  text-align: center;
}
</style>
