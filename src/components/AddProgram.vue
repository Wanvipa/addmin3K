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
      <label class="label">location : </label>
      <input class="input widthinput" type="text" v-model="location" >
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
        location: this.location,
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
