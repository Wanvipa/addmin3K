<template lang="html">
  <div class="app">
    <!-- ส่วนของกิจกรรมต่างๆ -->
        <div  class ="width-card"v-show="list.type==='Program'">
          <div class="card-content">
            <div class="media">
              <div class="media-content">
                <div class="tapprogram">
                  <p class="title is-5 text textblack"><i class="fa fa-list-alt" aria-hidden="true"></i>&nbsp;&nbsp;{{list.type}}</span>
                    <button type="button" @click="deleteEvent(list.id)">X</button></p>
                    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<small>{{timeout}}</small>
                </div>
              </div>
            </div>
            <div class="content sizefont"><br>
              {{list.message}}<br>
              <a :href="list.locationLink"><h5 class="subtitle is-6 ">location : {{list.location}}</a>
              <small>{{list.time}}</small>

            </div>
          </div>
        </div>
      </div>

</template>

<script>
export default {
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
