<style scoped>
.app-seccess{
  background: #fff;
  height: 100%;
}

    .app-seccess .header {
        padding-top: 80px;
    }

    .app-seccess .title-h {
        text-align: left;
        font-weight: bold;
        font-size: 20px;
        padding: 0 20px;
        padding-top: 40px;
    }

    .color-gray {
        line-height: 28px;
        text-align: left;
        padding: 0 20px;
    }

    .color-gray a {
        color: #217DF0;
    }

    .app-btn-primary {
        border-radius: 5px;
        background: #f2f3f7;
        color: #8492A6;
    }

    .app-btn {
        background: #f2f3f7;
        color: #8492A6;
    }

    .weui_cell_bd input {
        width: 100%;
        border: 0;
        outline: 0;
        -webkit-appearance: none;
        background-color: transparent;
        font-size: inherit;
        color: inherit;
        height: 1.46666667em;
        line-height: 1.46666667;
    }

    .weui_cell {
        margin: 30px 20px;
        padding: 14px 0;
        position: relative;
        display: flex;
        align-items: center;
        border-bottom: 1px solid #d9d9d9;
    }

    .weui_icon {
        margin-right: 10px;
        width: 20px;
        height: 20px;
        float: left;
    }

    .weui_cell_bd {
        width: 240px;
        float: left;
    }

    .active {
        background: #217DF0;
        color: #fff;
    }
</style>

<template>
    <div class="app-seccess">
        <!-- <div class="header">
          <icon type="success" class="icon_big"></icon></div>
        <div> -->
        <p class="title-h">最后一步</p>
        <p class="color-gray">我们已给您的对公银行账号<br> <span style="color:blue"> {{model.bankName}} {{model.bankAccount}} </span>转账了一笔随机金额，<br>请填写收到的具体金额以完成验证。</p>
        <div class="weui_cell">
            <div class="weui_icon">
                <img src="../../assets/img/pay-icon.png" style="width:20px;margin-right:15px;display:block" alt="手机号码"/>
            </div>
            <div class="weui_cell_bd weui_cell_primary">
                <input class="weui_input" type="number" v-model="model.amt" placeholder="请输入具体金额" @keyup="onKeyup" />
            </div>
        </div>
        <div class="btn-area" style="margin:20px 15px;">
            <input value="完成" type="button" class="weui-btn app-btn-primary" @click="confirmMoney" v-bind:class="{ active: Active}">
        </div>
        <div class="btn-area" style="margin:20px 15px;">
            <button class="weui-btn app-btn" @click="closeWindow">还没收到转账，稍后完成</button>
        </div>

    </div>

</template>


<script>
    import {Box, Icon} from '../../vux/index'
    import wx from 'weixin-js-sdk'

    export default {
        components: {
            Box,
            Icon
        },

        mounted(){

            
            this.$http.get("api/auth").then(({data}) => {
                if (data && 'SUBMITTED' == data.status) {
                    this.$router.push({path: "/enterprise/submitted"})
                    return;
                }

                let bankModel = {};
                Object.assign(bankModel, this.model, data);
                this.model = bankModel;
            });

        },

        data() {
            return {
                model: {bankName:'', bankAccount: "", amt: ''},
                Active: false,
                hasError: true
            }
        },
        methods: {
            onKeyup(){
                if (this.model.amt.length>0)
                {

                this.Active = true;

                }else{

                this.Active = false;
                
                }
                
            },
            confirmMoney() {
                
                if (!/(^(?!0+(?:\.0+)?$)(?:[1-9]\d*|0)(?:\.\d{2})?$)/.test(this.model.amt) ) {
                    this.$vux.toast.show({
                        text: '请输入大于0的两位小数',
                        type: "cancel"
                    });
                    return;
                }
                this.$root.showLoading = true;
                this.$http.post('api/auth/organ/check/transfer', this.model)
                    .then(({data}) => {
                        this.$root.showLoading = false
                        if (data._code == 200) {
                            this.$router.replace({path: "/enterprise/submitted"})
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
