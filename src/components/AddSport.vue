<template lang="html">
  <div class="app" >
      <p class="control">
        <label class="label">Time : </label>
        <input class="input widthinput" type="text" v-model="time" >

      </p>
      <p class="control">
        <label class="label">Sport : </label>
        <input class="input widthinput" type="text" v-model="sport" >
      </p>
      <p class="control">
        <label class="label">Location : </label>
        <input class="input widthinput" type="text" v-model="location" >
      </p>
      <p class="control">
        <label class="label">competition : </label>
        <input class="input widthinput" type="text" v-model="competition" >
      </p>
      <p class="control">
        <label class="label">Status : {{status}}</label>
        <span class="select">
          <select  v-model="status">
            <option>กำลังแข่งขัน</option>
            <option>พักเบรก</option>
            <option>เสร็จสิ้น</option>
          </select>
        </span>
      </p>
      <p class="control"><button class="button is-primary" @click="add">ADD</button></p>
  </div>
</template>

<script>
export default {
  props: ['addEvent'],
  data () {
    return {
      type: 'sport',
      time: '',
      sport: '',
      location: '',
      competition: '',
      status: ''
    }
  },
  computed: {},
  mounted () {},
  methods: {
    add () {
      var today = new Date()
      var timePost = today.getHours() + ':' + today.getMinutes()
      var data = {
        type: 'sport',
        time: this.time,
        location: this.location,
        sport: this.sport,
        competition: this.competition,
        status: this.status,
        total1: 0,
        total2: 0,
        timePost
      }
      this.addEvent(data)
      this.type = ''
      this.time = ''
      this.sport = ''
      this.location = ''
      this.competition = ''
      this.status = ''
    }
  },
  components: {}
}
</script>

<style lang="css">
.widthinput{
  width: 200px;
}
.app{
  text-align: center;
}
</style>
