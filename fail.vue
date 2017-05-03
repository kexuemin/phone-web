<style scoped>

    .app-warn {
        text-align: center;
        height: 100%;
        background: #fff;
    }

    .app-warn .header {
        padding: 30px;
    }

    .app-warn .title {
        padding: 5px;
    }
</style>

<template>
    <div class="app-warn">
        <div class="header">
            <box gap="30px 30px">
                <icon type="cancel" is-msg class="weui-icon weui_icon_warn weui-icon-warn weui-icon_msg"></icon>
            </box>
        </div>
        <div>
            <p class="color-gray">很抱歉</p>
            <p class="color-gray">你的企业基本信息有误！</p>
        </div>
    </div>
</template>


<script>
    import {Box, Icon} from '../../vux/index'

    export default {
        components: {
            Box,
            Icon
        }
    }
</script>
