<template lang="html">
  <div class="app">
    <!-- ส่วนของกิจกรรมต่างๆ -->
        <div  class ="width-card"v-show="list.type==='Program'">
          <div class="card-content">
            <div class="media">
              <div class="media-content">
                <div class="tap">
                  <img src="./event.png" class="tapstatus" alt="">
                  <a class="button is-primary buttdel"  @click="deleteEvent(list.id)">ลบ</a><br>
                  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<small class="sizedate">{{fromNow}}</small>
                </div><br>
              </div>
            </div>
            <div class="content sizefont"><br>
              <h5 class="subtitle is-5 ">{{list.message}}<br></h5>
              <a :href="list.locationLink"><h5 class="subtitle is-5 textlocation"><i class="fa fa-map-marker location" aria-hidden="true"></i> : {{list.location}}</a>
                {{date}}
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
      timestamp: '',
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
    date () {
      return this.list.time.substr(10, this.list.time.length - 13) + ' - ' + this.list.endTime
    },
    fromNow () {
      this.count
      this.timestamp = moment(this.list.time)
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
