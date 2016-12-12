<template lang="html">
  <div class="app" >
    <p class="control">
      <label class="label">Time : </label>
      <input class="input widthinput" type="text" v-model="time" >
    </p>
    <p class="control">
      <label class="label">message: </label>
      <input class="input widthinput" type="text" v-model="message" >
    </p>
    <p class="control">
      <label class="label">Location : </label>
      <span class="select">
        <select  v-model="location">
          <option :value="{link: 'https://goo.gl/maps/ihEyHNNVhDH2', name:'โดมแดง มหาวิทยาลัยเทคโนโลยีพระจอมเกล้าพระนครเหนือ'}">โดมแดง มหาวิทยาลัยเทคโนโลยีพระจอมเกล้าพระนครเหนือ</option>
          <option :value="{link: 'https://goo.gl/maps/ihEyHNNVhDH2', name:'สนามฟุตบอล'}">สนามฟุตบอล KMUTNB</option>
          <option :value="{link: 'https://goo.gl/maps/pcfvwmV3UWR2', name:'โรงยิม'}">โรงยิม</option>
          <option :value="{link: 'https://goo.gl/maps/YAqhKPyzNUw', name:'โรงอาหาร'}">โรงอาหาร</option>
          <option :value="{link: 'https://goo.gl/maps/C6izqXaKWKv', name:'ตึกคณะเทคโนโลยีและการจัดการอุตสาหกรรม ชั้น 4 B4-08'}">ตึกคณะเทคโนโลยีและการจัดการอุตสาหกรรม ชั้น 4 B4-08</option>
          <option :value="{link: 'https://goo.gl/maps/C6izqXaKWKv', name:'สนามแข่งกีฬา ตึกคณะเทคโนโลยีและการจัดการอุตสาหกรรม ชั้น 1'}">สนามแข่งกีฬา ตึกคณะเทคโนโลยีและการจัดการอุตสาหกรรม ชั้น 1</option>
          <option :value="{link: 'https://goo.gl/maps/49WJu3TxgBn', name:'สนามบาสเยื้องหน้าหอชาย'}">สนามบาสเยื้องหน้าหอชาย</option>
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
      type: 'Program',
      time: '',
      message: '',
      location: ''
    }
  },
  computed: {},
  mounted () {},
  methods: {
    add () {
      var today = new Date()
      var timePost = today.getHours() + ':' + today.getMinutes()
      var data = {
        type: 'Program',
        time: this.time,
        message: this.message,
        locationLink: this.location.link,
        location: this.location.name,
        timePost
      }
      this.addEvent(data)
      this.type = ''
      this.time = ''
      this.message = ''
      this.location = ''
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
