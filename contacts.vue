<style scoped>
    .header {
        background: #fff;
    }

    .header-step {
        padding: 10px 15px;
    }

    .weui-cells__title {
        margin: 0;
        height: 40px;
        line-height: 40px;
        color: #475568;
        font-weight: bold;
        background: #f2f3f7;
    }

    .weui-cells__title span {
        color: #bac5d4;
        font-weight: normal;
    }

    .weui-cell_bd {
        width: 240px;
    }

    .app-btn-primary {
        border-radius: 5px;
        background: #217DF0;
        color: #fff;
    }

    .content {
        background: #fff;
    }
</style>
<template>
    <div>
        <div class="header">
            <!-- <app-step :step="3"></app-step> -->
            <div class="header-step">
                <img src="../../assets/img/flow/step4.png" style="width:100%;"/>
            </div>
        </div>
        <div class="page" style="padding-bottom:60px;">
            <div class="content">
                <div class="weui-cells__title">财务联系人</div>
                <div class="weui-cell">
                    <div class="weui-cell__bd">
                        <label class="weui-label">姓名</label>
                    </div>
                    <div class="weui-cell_bd ">
                        <input class="weui-input" type="text" placeholder="请输入姓名" v-input-change="model.cfoName"
                               v-model="model.cfoName"/>
                    </div>
                </div>
                <div class="weui-cell">
                    <div class="weui-cell__bd">
                        <label class="weui-label">手机号码</label>
                    </div>
                    <div class="weui-cell_bd ">
                        <input class="weui-input" type="tel" placeholder="请输入手机号码" maxlength="11"
                               v-input-change="model.cfoPhone" v-model="model.cfoPhone"/>
                    </div>
                </div>
                <div class="weui-cell">
                    <div class="weui-cell__bd">
                        <label class="weui-label">电子邮箱</label>
                    </div>
                    <div class="weui-cell_bd ">
                        <input class="weui-input" type="email" placeholder="请输入邮箱（用于接收对账通知）" maxlength="50"
                               v-model="model.cfoEmail" v-input-change="model.cfoEmail"/>
                    </div>
                </div>
            </div>
            <div class="content">
                <!-- <selector title="关系" :value="model.emergContactRelation" @on-change="emergContactRelationChangeEvent" :options="emgerContactRelation"></selector> -->
                <div class="weui-cells__title">总经理<span>（若与法人相同，则填写第二联系人）</span></div>
                <div class="weui-cell">
                    <div class="weui-cell__bd">
                        <label class="weui-label">姓名</label>
                    </div>
                    <div class="weui-cell_bd ">
                        <input class="weui-input" type="text" placeholder="请输入名字" v-model="model.gmName"
                               v-input-change="model.gmName"/>
                    </div>
                </div>
                <div class="weui-cell">
                    <div class="weui-cell__bd">
                        <label class="weui-label">手机号码</label>
                    </div>
                    <div class="weui-cell_bd ">
                        <input class="weui-input" type="tel" placeholder="请输入手机号码" maxlength="11"
                               v-model="model.gmPhone" v-input-change="model.gmPhone"/>
                    </div>
                </div>
                <div class="weui-cell">
                    <div class="weui-cell__bd">
                        <label class="weui-label">电子邮箱</label>
                    </div>
                    <div class="weui-cell_bd ">
                        <input class="weui-input" type="email" placeholder="请输入邮箱（用于接收对账通知）" maxlength="50"
                               v-model="model.gmEmail" v-input-change="model.gmEmail"/>
                    </div>
                </div>
            </div>
            <div class="btn-area" style="margin:20px 15px;">
                <button class="weui-btn app-btn-primary" @click="saveUserInfo">下一步</button>
            </div>
        </div>
    </div>

</template>

<script>
    import {
        Selector
    } from '../../vux/index'

    export default {
        components: {
            Selector
        },

        mounted(){
            this.$http.get("api/auth").then(({data}) => {
                if (data && ('PENDING_HISTORY' ==data.status || 'SUBMITTED' == data.status)) {
                    this.$router.push({path: "/enterprise/submitted"});
                    return;
                }
            });

            this.$http.get("api/auth/extensions").then(({data}) => {
                let bankModel = {};
                Object.assign(bankModel, this.model, data);
                this.model = bankModel;
            });
        },
        data() {
            return {
                model: {
                    status: '',
                    cfoPhone: '',
                    cfoEmail: '',
                    gmName: '',
                    gmPhone: '',
                    gmEmail: ''
                }
            }
        },
        methods: {
            saveUserInfo() {
                if (this.model.cfoName == "" || (!/^[\u4e00-\u9fa5]+$/.test(this.model.cfoName) )) {
                    this.$vux.toast.show({
                        text: '请输入中文姓名',
                        type: "cancel"
                    })
                    return;
                } else if (this.model.cfoPhone == "" || (!/^1[3,5,8,7]\d{9}$/.test(this.model.cfoPhone) )) {
                    this.$vux.toast.show({
                        text: '请输入正确的手机号',
                        type: "cancel"
                    })
                    return;
                } else if (this.model.cfoEmail == "" || (!/^[a-zA-Z0-9_-]+@[a-zA-Z0-9_-]+(\.[a-zA-Z0-9_-]+)+$/.test(this.model.cfoEmail) )) {
                    this.$vux.toast.show({
                        text: '请输入正确的邮箱',
                        type: "cancel"
                    })
                    return;
                } else if (this.model.gmName == "" || (!/^[\u4e00-\u9fa5]+$/.test(this.model.gmName) )) {
                    this.$vux.toast.show({
                        text: '请输入中文姓名',
                        type: "cancel"
                    })
                    return;
                } else if (this.model.gmPhone == "" || (!/^1[3,5,8,7]\d{9}$/.test(this.model.gmPhone) )) {
                    this.$vux.toast.show({
                        text: '请输入正确的手机号',
                        type: "cancel"
                    })
                    return;
                } else if (this.model.gmEmail == "" || (!/^[a-zA-Z0-9_-]+@[a-zA-Z0-9_-]+(\.[a-zA-Z0-9_-]+)+$/.test(this.model.gmEmail) )) {
                    this.$vux.toast.show({
                        text: '请输入正确的邮箱',
                        type: "cancel"
                    })
                    return;
                }

                this.$root.showLoading = true;
                this.$http.post('api/auth/enterprise/contacts', this.model)
                    .then(({data}) => {
                        this.$root.showLoading = false
                        if (data._code == 200) {
                            if (data.params) {
                                this.$router.push({path: "/enterprise/last"})
                            } else {
                                this.$router.push({path: "/enterprise/key"})
                            }

                        } else if (data._code == 411) {
                            this.$router.push({
                                path: "/employee/warn"
                            })
                        } else {
                            this.$vux.toast.show({
                                text: data._msg,
                                type: "cancel"
                            })
                        }
                    })
            }
        }
    }
</script>
