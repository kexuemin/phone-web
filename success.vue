<style scoped>
    .app-seccess {
        text-align: center;
        height: 100%;
        background: #fff;
    }

    .app-seccess .header {
        padding-top: 80px;
    }

    .app-seccess .title {
        padding: 5px;
        margin-top: 10px;
    }
</style>

<template>
    <div class="app-seccess">
        <div>
            <x-header :left-options="{showBack: false}"><a @click="closeWindow" slot="right">X</a>
            </x-header>
        </div>
        <div class="header">
            <icon type="success" class="icon_big"></icon>
        </div>
        <div>
            <p class="title">已成授权成功</p>
        </div>
    </div>
</template>


<script>
    import {Box, Icon, XHeader, Cell} from '../../vux/index'
    import wx from 'weixin-js-sdk'

    export default {
        components: {
            Box,
            Icon,
            XHeader
        },
        methods: {
            closeWindow() {
                console.log("sss")
                wx.closeWindow();
            }
        }
    }
</script>
