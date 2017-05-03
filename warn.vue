<style scoped>
.app-warn{
      text-align: center;
    height: 100%;
    background: #fff;
}
.app-warn .header{
 padding: 30px;
}
.app-warn .title{padding:5px; }
</style>

<template>
  <div class="app-warn">
    <div class="header">
      <icon type="safe_warn" class="icon_big weui-icon weui_icon_safe_warn weui-icon-safe-warn weui-icon_msg" ></icon>
    </div>
    <div>
      <p class="title">很抱歉</p>
      <p class="color-gray">您不是内测邀请用户，暂不支持</p>
    </div>
  </div>
</template>


<script>
import { Box, Icon } from '../../vux/index'

export default {
  components: {
    Box,
    Icon
  }
}
</script>
