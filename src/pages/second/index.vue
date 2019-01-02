<template>
  <div class="container">
    <span>{{motto}}</span>
  </div>
</template>

<script>

export default {
  data () {
    return {
      motto: '这是第二个页面',
    }
  },

  components: {
  },

  methods: {
  },
  mounted(){
    console.log(this.$root.$mp.query)
    console.log(this.$getParams());
  },
  created () {
  }
}
</script>

<style lang="scss" scoped>
.container{
  span{
    color: red;
  }
}
</style>
