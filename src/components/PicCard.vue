<template lang="html">
  <div class="app">
    <div  class ="width-card"v-show="list.type==='Picture'">
      <div class="card-image">
        <figure class="image is-3by2">
          <img :src="list.picture" alt="">
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <div class="tap">
              <p class="title is-5 ">
                <i class="fa fa-picture-o" aria-hidden="true"></i>
                &nbsp;{{list.type}}<br>
                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<small>{{timeout}}</small>
                <button type="button" @click="deleteEvent(list.id)">X</button></p>
            </p>
          </div>
        </div>
      </div>
      <div class="content "><br>
        <h5 class="subtitle is-5 ">{{list.caption}}<br></h5>
        <small class="sizedate">{{list.time}}</small>
      </div>
    </div>
  </div>
  </div>
</template>

<script>
export default {
  name: 'PicCard',
  props: ['list', 'deleteEvent'],
  data () {
    return {}
  },
  computed: {
    timeout () {
      var time = ''
      if (this.list.timePost) {
        var timePost = this.list.timePost.split(':')
        var timeAgo = parseInt(timePost[0]) * 60 + parseInt(timePost[1])
        var today = new Date()
        var timeNow = today.getHours() * 60 + today.getMinutes()
        if (timeAgo === timeNow) {
          time = 'เมื่อสักครู่นี้'
        } else {
          if (timeNow - timeAgo < 60) {
            time = (timeNow - timeAgo) + 'นาทีที่แล้ว'
          } else {
            time = (parseInt(timeNow / 60) - parseInt(timeAgo / 60)) + 'ชั่วโมงที่แล้ว'
          }
        }
      }
      return time
    }
  },
  mounted () {},
  methods: {},
  components: {}
}
</script>

<style lang="css">

</style>
