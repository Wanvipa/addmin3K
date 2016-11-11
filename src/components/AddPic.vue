<template lang="html">
  <div class="app" >
    <p class="control">
      <label class="label">Time : </label>
      <input class="input widthinput" type="text" v-model="time" >
    </p>
    <p class="control">
      <label class="label">picture : </label>
      <input class="input widthinput" type="text" v-model="picture" >
    </p>
    <p class="control">
      <label class="label">Caption : </label>
      <input class="input widthinput" type="text" v-model="caption" >
    </p>
    <p class="control"><button class="button is-primary" @click="add">ADD</button></p>
  </div>
</template>

<script>
export default {
  props: ['addEvent'],
  data () {
    return {
      type: 'Picture',
      time: '',
      picture: '',
      caption: ''
    }
  },
  computed: {},
  mounted () {},
  methods: {
    add () {
      var today = new Date()
      var timePost = today.getHours() + ':' + today.getMinutes()
      var data = {
        type: 'Picture',
        time: this.time,
        picture: this.picture,
        caption: this.caption,
        timePost
      }
      this.addEvent(data)
      this.type = ''
      this.time = ''
      this.picture = ''
      this.caption = ''
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
