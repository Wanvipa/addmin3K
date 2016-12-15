<template lang="html">
  <div class="app" >
    <p class="control">
      <label class="label">Time : </label>
      <vue-timepicker v-model="timeValue"></vue-timepicker>
    </p>
    <p class="control">
      <label class="label">Time S/F: </label>
      <input class="input widthinput" type="text" v-model="message" >
    </p>
    <p class="control">
      <label class="label">message: </label>
      <input class="input widthinput" type="text" v-model="message" >
    </p>
    <p class="control">
      <label class="label">Location : </label>
      <span class="select">
        <select  v-model="location">
          <option :value="{link: 'https://goo.gl/maps/utxXD2vQrAv', name:'อาคารศูย์กีฬาเฉลิมพระเกียรติ'}">อาคารศูย์กีฬาเฉลิมพระเกียรติ</option>
          <option :value="{link: 'https://goo.gl/maps/ihEyHNNVhDH2', name:'สนามฟุตบอล'}">สนามฟุตบอล KMUTNB</option>
          <option :value="{link: 'https://goo.gl/maps/YAqhKPyzNUw', name:'อาคารโรงอาหาร'}">อาคารโรงอาหาร</option>
          <option :value="{link: 'https://goo.gl/maps/C6izqXaKWKv', name:'ตึกคณะเทคโนโลยีและการจัดการอุตสาหกรรม'}">ตึกคณะเทคโนโลยีและการจัดการอุตสาหกรรม</option>
          <option :value="{link: 'https://goo.gl/maps/49WJu3TxgBn', name:'สนามบาสเยื้องหน้าหอชาย'}">สนามบาสเยื้องหน้าหอชาย</option>
        </select>
      </span>
    </p>
    <p class="control"><button class="button is-primary" @click="add">ADD</button></p>
  </div>
</template>

<script>
import VueTimepicker from 'vue2-timepicker'
export default {
  props: ['addEvent'],
  data () {
    return {
      type: 'Program',
      time: '',
      timeSF: '',
      message: '',
      location: '',
      timeValue: {
        HH: '08',
        mm: '10',
        ss: '00'
      }
    }
  },
  computed: {},
  mounted () {},
  methods: {
    add () {
      var today = new Date()
      var dayTime = today.getFullYear() + '-' + (today.getMonth() + 1) + '-' + today.getDate() + ' ' + this.timeValue.HH + ':' + this.timeValue.mm + ':00'
      console.log(dayTime)
      var data = {
        type: 'Program',
        time: dayTime,
        message: this.message,
        locationLink: this.location.link,
        location: this.location.name
      }
      this.addEvent(data)
      this.time = ''
      this.timeSF = ''
      this.message = ''
      this.location = ''
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
.app{
  text-align: center;
}
</style>
