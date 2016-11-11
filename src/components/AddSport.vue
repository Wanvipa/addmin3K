<template lang="html">
  <div class="app" >
      <p class="control">
        <label class="label">Time : </label>
        <input class="input widthinput" type="text" v-model="time" >
      </p>
      <p class="control">
        <label class="label">Sport : {{sport}}</label>
        <span class="select">
          <select  v-model="sport">
            <option>Basketball</option>
            <option>Football</option>
            <option>vallaball</option>
            <option>Batminton</option>
            <option>E-Sport</option>
          </select>
        </span>
      </p>
      <p class="control">
        <label class="label">Type : {{sport}}</label>
        <span class="select">
          <select  v-model="kind">
            <option>ชายเดี่ยว</option>
            <option>หญิงเดี่ยว</option>
            <option>คู่ผสม</option>
            <option></option>

          </select>
        </span>
      </p>
      <p class="control">
        <label class="label">Location : </label>
        <input class="input widthinput" type="text" v-model="location" >
      </p>
      <p class="control">
          <label class="label">competition : {{competition}}</label>
          <span class="select">
          <select v-model="competition">
            <option>KMUTNB : KMLIT</option>
            <option>KMUTT : KMUTNB</option>
            <option>KMILT : KMUTT</option>
          </select>
        </span>
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
      kind: '',
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
        kind: this.kind,
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
      this.kind
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

</style>
