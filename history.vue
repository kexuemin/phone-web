<template>
    <div class="btn-area" style="margin:20px 15px;">
        <button class="weui-btn app-btn-primary" @click="uploadHistoryData">上传历史数据</button>
    </div>

</template>


<script>
    import Vue from 'vue'
    import {queryString} from '../../utils/utils'
    export default {

        mounted() {
            let code = queryString("code");
            let state = queryString("state");
            if (!window.sessionStorage.getItem("token") && code) {
                this.$http.get('api/wechat/token?code=' + code + '&state=' + state).then(({data}) => {
                    if (data.code == 200) {
                        window.sessionStorage.setItem("token", data.token);
                        Vue.http.headers.common['Authorization'] = 'Basic ' + data.token;
                    }
                })
            } else {
                let token = window.sessionStorage.getItem("token");
                console.log(token)
                Vue.http.headers.common['Authorization'] = 'Basic ' + token;
            }
        },

        methods: {
            uploadHistoryData() {
                this.$vux.loading.show({text: '数据上传中...'});
                this.$root.showLoading = true;
                this.$http.get('api/auth/mock/history/data', this.model)
                    .then(({data}) => {
                        this.$root.showLoading = false;
                        this.$vux.loading.hide();
                        if (data._code == 200) {
                            this.$vux.toast.show({
                                text: "上传成功",
                                type: "success"
                            })
                        } else {
                            
                            this.$vux.toast.show({
                                text: data._msg,
                                type: "cancel"
                            })
                        }
                    });
            },
            closeWindow() {
                wx.closeWindow();
            }
        }
    }
</script>
