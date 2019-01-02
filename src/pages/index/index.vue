<template>
  <div class="container">
    <span>{{motto}}</span>
    <a href="/pages/second/main">第二页</a>
    <button @click="click">按钮</button>


    <div v-if="showAuthSetting" class="ui-dialog">
      <div class="ui-mask"></div>
      <div class="ui-confirm" style="background:#fff;border-radius:10rpx">
        <div class="modelTitle">
          获取微信授权信息
        </div>
        <div class="modelBody">微信登录需要获取您的用户信息，请前往设置</div>
        <div>
          <button open-type="getUserInfo" class="agree" lang="zh_CN">去设置</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import userModel from '@M/userModel'

export default {
  data () {
    return {
      motto: 'Hello world',
      showAuthSetting: false
    }
  },

  components: {
  },

  methods: {
    init(){
      // 登录
      userModel.login(()=>{
      });
    },
    click(){
      this.$post({
        url:"/sn/user/login.do"
      })
      // this.$toPage('/pages/second/main', {
      //   id: 223,
      //   data: 'data',
      //   object: {
      //     obj: '1'
      //   },
      //   array: ['1','2']
      // })
    }
  },
  mounted(){
  },
  created () {
    
  },

  onLoad(params) {
      let self = this;
      wx.getSetting({
        success: (res) => {
          //判断用户已经授权。不需要弹框
          if(res.authSetting['scope.userInfo']){
            this.showAuthSetting = false
            this.init(params);
          }else{//没有授权需要弹框
            this.showAuthSetting = true
          }
        },
        fail: () => {
          this.toast('系统提示:网络错误')
        }
      })
      
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
