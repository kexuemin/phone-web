<style scope>
body{
  background: #fff;
}
.app-seccess{text-align: center;height: 100%;background: #fff;}
.app-seccess .header{
 padding-top: 80px;
}
.app-seccess .title{padding:5px;margin-top:10px; }
.close{
  position: absolute;
  right: 12px;
  top: 5px;
  color: #217DF0;
}
</style>

<template>
  <div class="app-seccess">
    <a @click="closeWindow" class="close">X</a>
    <div class="header">
      <icon type="success" class="icon_big"></icon>
      
      </div>
    <div>
      <p class="title">已成功提交授权申请</p>
      <p class="color-gray">您将在4小时内收到审批结果</p>
    </div>
  </div>
</template>


<script>
import { Box, Icon } from '../../vux/index'

export default {
  components: {
    Box,
    Icon
  },
  methods: {
            closeWindow() {
                wx.closeWindow();
            }
        }
}
</script>
