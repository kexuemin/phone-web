<template>

<div class="weui_loading_toast" >
  <div class="weui_mask_transparent"></div>
   <div class="weui_toast">
     <i class="weui-loading weui-icon_toast"></i>
   <p class="weui_toast_content">Start processing</p></div></div>
</template>

<script>
export default {
  ready () {
    setTimeout(() => {
      this.$router.replace({path: '/event'})
    }, 500)
  }
}
</script>
