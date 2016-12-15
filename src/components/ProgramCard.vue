<template lang="html">
  <div class="app">
    <!-- ส่วนของกิจกรรมต่างๆ -->
        <div  class ="width-card"v-show="list.type==='Program'">
          <div class="card-content">
            <div class="media">
              <div class="media-content">
                <div class="tap">
                  <img src="./event.png" class="tapstatus" alt="">
                  <a class="button is-primary buttdel"  @click="deleteEvent(list.id)">ลบ</a>
                  </div>
              </div>
            </div>
            <div class="content sizefont"><br>
              <h5 class="subtitle is-5 ">{{list.message}}<br></h5>
              <a :href="list.locationLink"><h5 class="subtitle is-5 textlocation">สถานที่ : {{list.location}}</a>
             <small class="sizedate">{{list.time}}&nbsp;{{fromNow}}</small>
            </div>
          </div>
        </div>
      </div>

</template>

<script>
/* global moment */
export default {
  props: ['list', 'deleteEvent'],
  data () {
    return {
      timestamp: moment(this.list.time),
      count: 0
    }
  },
  created () {
    let vm = this
    setInterval(() => {
      vm.count++
    }, 1000)
  },
  computed: {
    fromNow () {
      this.count
      return moment(this.timestamp).fromNow()
    }
  },
  mounted () {
    moment.lang('th')
  },
  methods: {},
  components: {}
}
</script>

<style lang="css">
</style>
