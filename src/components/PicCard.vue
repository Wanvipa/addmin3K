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
              <img src="./photo.png" class="tapstatus"alt="">
              <a class="button is-primary buttdel"  @click="deleteEvent(list.id)">ลบ</a>
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
  },
  mounted () {},
  methods: {},
  components: {}
}
</script>

<style lang="css">

</style>
