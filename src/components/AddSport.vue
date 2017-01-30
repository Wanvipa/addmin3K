<template lang="html">
  <div class="app" >
      <p class="control">
        <label class="label">Time : </label>
        <vue-timepicker v-model="timeValue"></vue-timepicker>
      </p>
      <p class="control">
        <label class="label">Sport : {{sport}}</label>
        <span class="select">
          <select  v-model="sport">
            <option>Basketball</option>
            <option>Football</option>
            <option>Volleyball</option>
            <option>Badminton</option>
            <option>E-Sport</option>
            <option>Table Tennis</option>
          </select>
        </span>
      </p>
      <p class="control">
        <label class="label">Type : {{kind}}</label>
        <span class="select">
          <select  v-model="kind">
            <option>ชายเดี่ยว</option>
            <option>หญิงเดี่ยว</option>
            <option>คู่ผสม</option>
            <option>ชาย</option>
            <option>หญิง</option>
          </select>
        </span>
      </p>
      <p class="control">
        <label class="label">Location : </label>
        <span class="select">
          <select  v-model="location">
            <option :value="{link: 'https://goo.gl/maps/utxXD2vQrAv', name:'อาคารศูนย์กีฬาเฉลิมพระเกียรติ'}">อาคารศูนย์กีฬาเฉลิมพระเกียรติ</option>
            <option :value="{link: 'https://goo.gl/maps/ihEyHNNVhDH2', name:'สนามฟุตบอล'}">สนามฟุตบอล KMUTNB</option>
            <option :value="{link: 'https://goo.gl/maps/C6izqXaKWKv', name:'ตึกคณะเทคโนโลยีและการจัดการอุตสาหกรรม'}">ตึกคณะเทคโนโลยีและการจัดการอุตสาหกรรม</option>
            <option :value="{link: 'https://goo.gl/maps/49WJu3TxgBn', name:'สนามบาสเยื้องหน้าหอชาย'}">สนามบาสเยื้องหน้าหอชาย</option>
          </select>
        </span>
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
import VueTimepicker from 'vue2-timepicker'
export default {
  props: ['user', 'addEvent'],
  data () {
    return {
      type: 'sport',
      sport: '',
      kind: '',
      location: '',
      competition: '',
      status: '',
      timeValue: {
        HH: '08',
        mm: '10',
        ss: '00'
      }
    }
  },
  computed: {},
  mounted () {
  },
  methods: {
    add () {
      var today = new Date()
      var dayTime = today.getFullYear() + '-' + (today.getMonth() + 1) + '-' + today.getDate() + ' ' + this.timeValue.HH + ':' + this.timeValue.mm + ':00'
      console.log(dayTime)
      var data = {
        type: 'sport',
        time: dayTime,
        location: this.location.name,
        locationLink: this.location.link,
        sport: this.sport,
        kind: this.kind,
        competition: this.competition,
        status: this.status,
        total1: 0,
        total2: 0,
        admin: this.user.displayName
      }
      this.addEvent(data)
      this.type = ''
      this.sport = ''
      this.kind = ''
      this.location = ''
      this.competition = ''
      this.status = ''
    }
  },
  components: {
    VueTimepicker
  }
}
</script>

<style lang="css">
.widthinput{
  width: 200px;
}

</style>
