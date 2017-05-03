<style>
    .header {
        background: #fff;
    }

    .header-step {
        padding: 10px 15px;
    }

    .weui-cells_title {
        margin: 0;
        height: 20px;
        line-height: 20px;
        color: #475568;
        font-weight: bold;
        background: #f2f3f7;
        font-size: 14px;
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

    .weui-cell:before {
        /*border-top: 0;*/
    }

    .weui-cells:before {
        border-top: 0;
    }

    .weui-cells:after {
        border-bottom: 0;
    }

    .weui-cell {
        /*border-bottom: 1px solid #f2f3f7;*/
    }

    .weui-label {
        width: 115px;
    }

</style>
<template>
    <div>
        <div class="header">
            <!-- <app-step :step="3"></app-step> -->
            <div class="header-step">
                <img src="../../assets/img/flow/step2.png" style="width:100%;"/>
            </div>
        </div>
        <group class="weui-cells_form">
            <div class="weui-cell">
                <div class="weui-cell_hd">
                    <label class="weui-label">企业名称</label>
                </div>
                <div class="weui-cell__bd weui-cell_primary">
                    <input class="weui-input" type="text" v-input-change="model.name" placeholder="请输入企业名称"
                           v-model="model.name"/>
                </div>
            </div>
            <div class="weui-cell">
                <div class="weui-cell_hd">
                    <label class="weui-label">企业法人</label>
                </div>
                <div class="weui-cell__bd weui-cell_primary">
                    <input class="weui-input" type="text" v-input-change="model.legalPersonName" placeholder="请输入法人名字"
                           v-model="model.legalPersonName"/>
                </div>
            </div>
            <div class="weui-cell">
                <div class="weui-cell_hd">
                    <label class="weui-label">营业执照注册号</label>
                </div>
                <div class="weui-cell_bd ">
                    <input class="weui-input" type="text" placeholder="请输入营业执照注册号码"
                           v-input-change="model.creditCode" v-model="model.creditCode" maxlength="18"
                           onBlur="this.value=this.value.toUpperCase()"/>
                </div>
            </div>
            <x-address style="border:0;" :title="title" v-model="addressCode" :list="addressData"
                       placeholder="请选择地址"></x-address>
            <div class="weui-cell">
                <div class="weui-cell_hd">
                    <label class="weui-label">详细经营地址</label>
                </div>
                <div class="weui-cell__bd weui-cell_primary">
                    <input class="weui-input" type="text" v-input-change="model.address" placeholder="请输入详细经营地址"
                           v-model="model.address"/>
                </div>
            </div>

        </group>
        <div class="btn-area" style="margin:20px 15px;">
            <button class="weui-btn app-btn-primary" @click="saveUserInfo">下一步</button>
        </div>
    </div>
</template>

<script>
    import {
        Selector, XAddress, ChinaAddressData, Group, Cell, Value2nameFilter as value2name
    } from '../../vux/index'

    export default {
        components: {
            Selector, XAddress, ChinaAddressData, Group, Cell
        },

        mounted(){
            this.$http.get("api/auth").then(({data}) => {
                let bankModel = {};
                Object.assign(bankModel, this.model, data);
                this.model = bankModel;
                if (this.model.provinceCode && this.model.cityCode && this.model.districtCode) {
                    this.addressCode = [this.model.provinceCode, this.model.cityCode, this.model.districtCode];
                }
            });

            this.$http.get("api/auth/extensions").then(({data}) => {
                this.model.legalPersonName = data.legalPersonName;
            });
        },

        data() {
            return {
                model: {
                    status: '',
                    name: '',
                    creditCode: '',
                    address: '',
                    provinceCode: '',
                    cityCode: '',
                    districtCode: '',
                    legalPersonName: '',
                    integrated: '',
                    taxCode: '',
                    orgCode: ''
                },
                addressCode: [],
                title: '实际经营地址',
                addressData: ChinaAddressData
            }
        },
        methods: {
            saveUserInfo() {
                if (this.model.name == "") {
                    this.$vux.toast.show({
                        text: '请输入企业名称',
                        type: "cancel"
                    })
                    return;
                }
                if (this.model.legalPersonName == "" || (!/^[\u4e00-\u9fa5]+$/.test(this.model.legalPersonName) )) {
                    this.$vux.toast.show({
                        text: '请输入企业法人中文名字',
                        type: "cancel"
                    })
                    return;
                }

                if (this.model.creditCode == "" || (this.model.integrated == 'Y' && (!/^[a-zA-Z0-9]{18}$/.test(this.model.creditCode)))
                    || (this.model.integrated == 'N' && (!/^[a-zA-Z0-9]{15}$/.test(this.model.creditCode)))) {
                    this.$vux.toast.show({
                        text: '请输入正确的营业执照注册号',
                        type: "cancel"
                    })
                    return;
                }
                if (this.model.address == "") {
                    this.$vux.toast.show({
                        text: '请输入详细经营地址',
                        type: "cancel"
                    })
                    return;
                }

                this.$root.showLoading = true;
                this.model.provinceCode = this.addressCode[0];
                this.model.cityCode = this.addressCode[1];
                this.model.districtCode = this.addressCode[2];
                this.$http.post('api/auth/enterprise/infos', this.model)
                    .then(({
                               data
                           }) => {
                        this.$root.showLoading = false
                        if (data._code == 200) {
                            this.$router.push({
                                path: "/enterprise/bank",
                                query: {
                                    orderId: this.model.orderId
                                }
                            })
                        } else if (data._code == 411) {
                            this.$router.push({
                                path: "/employee/fail",
                                query: {
                                    orderId: this.model.orderId
                                }
                            })
                        } else {
                            this.$vux.toast.show({
                                text: data._msg,
                                type: "cancel"
                            })
                        }
                    })
            }
        },
        getName (value) {
            return value2name(value, ChinaAddressData)
        }
    }
</script>
