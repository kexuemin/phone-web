<style scoped>
    .pic-up {
        width: 92.5%;
        margin: 0 auto;
        padding: 10px 0px;
    }

    .pic-up li.row {
        margin-top: 5px;
        list-style: none;
        position: relative;
    }

    .pic-up .exp-pic {
        position: relative;
        width: 48.31%;
        padding-top: 28.69%;
    }

    .pic-up .exp-pic img {
        position: absolute;
        left: 0;
        top: 0;
        display: block;
        width: 100%;
        height: 100%;
    }

    .pic-up .take-pic {
        position: absolute;
        right: 0px;
        top: 0px;
        width: 48.31%;
        padding-top: 28.69%;
        background: #fff;
        overflow: hidden;
    }

    .pic-up .take-pic lable {
        position: absolute;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        border: 0;
        outline: none;
        z-index: 1;
    }

    .exp-pic-tip {
        position: absolute;
        top: 38%;
        left: 50%;
        width: 80px;
        margin-left: -40px;
        font-size: 12px;
        background: #000;
        color: #fff;
        text-align: center;
        border-radius: 4px;
        opacity: 0.5;
        padding: 0px 5px;
    }

    .take-pic strong {
        position: absolute;
        left: 0;
        top: 70%;
        width: 100%;
        color: #999;
        margin-top: -0.95rem;
        text-align: center;
    }

    .take-pic img {
        position: absolute;
        left: 0;
        top: 0;
        width: 100%;
        z-index: 2;
    }

    .header {
        background: #fff;
    }

    .header-step {
        padding: 10px 15px;
    }

    .app-btn-primary {
        border-radius: 5px;
        background: #217DF0;
        color: #fff;
    }

    .weui-cells {
        margin-top: 0;
    }

    .weui-cells_form {
        /*margin-top: 20px;*/
    }

    /*.weui-cells:before{
        height: 0;
        border-top:0;
    }*/
    .weui-cell_access {
        padding-left: 0;
    }

    .vux-cell-box:before {
        border-top: 0;
    }

    .vux-popup-picker-select span {
        display: block;
        text-align: left;
        color: #000;
    }

    .weui-cell {
        padding-left:;
    }

    .vux-selector.weui-cell_select-after {
        /*margin-left: 15px;
        padding-left: 0;*/
        /*border-top: .5px solid #D9D9D9;*/
    }

    .weui-cell:after {
        content: " ";
        position: absolute;
        left: 0;
        top: 0;
        width: 100%;
        height: 1px;
        border-top: 1px solid #D9D9D9;
        color: #D9D9D9;
        transform-origin: 0 0;
        transform: scaleY(0.5);
        left: 15px;
    }

    .weui-cells_form input {
        color: #000;
    }
</style>

<template>

    <div>
        <div class="header">
            <div class="header-step">
                <img src="../../assets/img/flow/step3.png" style="width:100%;"/>
            </div>
        </div>
        <!-- <div class="weui-cells_title"></div> -->
        <group class="weui-cells_form">
            <div class=" weui-cell_primary">
                <selector title="开户行" placeholder="请选择开户行" :options="bankCodeList"
                          @on-change="branchChangeEvent" :value="model.bankCode"></selector>
            </div>
            <!-- <group style="border:0;padding-left:15px;"> -->
            <x-address style="border:0;" title="地址" v-model="addressCode" :list="addressData"
                       placeholder="请选择地址"></x-address>
            <!-- </group> -->

            <div class="weui-cell__bd weui-cell_primary">
                <selector id="bankCodeId" title="支行" placeholder="请选择支行" @on-change="bankCodeChangeEvent"
                          :options="branchCodeList"
                          v-model="model.bankUnionNo"></selector>
            </div>
            <div class="weui-cell">
                <div class="weui-cell_hd">
                    <label class="weui-label">账号</label>
                </div>
                <div class="weui-cell__bd weui-cell_primary">
                    <input class="weui-input" type="number" placeholder="请输入储蓄卡号"
                           v-model="model.bankAccount"/>
                </div>
            </div>
        </group>
        <div class="btn-area" style="margin:20px 15px;">
            <button class="weui-btn app-btn-primary" @click="saveBank">下一步</button>
        </div>
    </div>
</template>

<script>
    import {key2value} from '../../utils/selectorUtils'
    import {Group, XAddress, Selector, ChinaAddressDataV} from '../../vux/index'

    export default {
        components: {
            Group,
            Selector, XAddress, ChinaAddressDataV
        },

        created(){
            this.$http.get("api/auth/bank/infos").then(({data}) => {
                data.params.bankCodeList.forEach((v) => {
                    this.bankCodeList.push({key: v.value, value: v.name})
                });

                data.params.branchCodeList.forEach((v) => {
                    this.branchCodeList.push({key: v.unionNo, value: v.bankName})
                });
                let bankModel = {};
                Object.assign(bankModel, this.model, data.params.enterpriseApply);
                this.model = bankModel;

                if (this.model.bankProvinceCode && this.model.bankCityCode) {
                    this.addressCode = [this.model.bankProvinceCode, this.model.bankCityCode];
                }

            });
        },

        data() {
            return {
                price: 0,
                model: {
                    bankCode: "",
                    bankName: '',
                    bankBranchName: '',
                    bankUnionNo: '',
                    bankAccount: "",
                    bankProvinceCode: "",
                    bankCityCode: ""
                },
                addressCode: [],
                upload: {
                    bankPhoto: "",
                    showUpload: true
                },
                bankCodeList: [],
                selectedBank: [],
                branchCodeList: [],
                showBank: false,
                loadingBank: false,
                addressData: ChinaAddressDataV
            }
        },

        watch: {
            addressCode: function (val, oldVal) {
                if (oldVal != val) {
                    let bankrollCode = val[1];
                    if (this.branchCodeList && this.branchCodeList.length == 1 && this.branchCodeList[0].key == this.model.bankUnionNo) {
                    } else {
                        this.branchCodeList = [];
                    }
                    this.$http.get("api/system/bank/union/numbers?bankrollCode=" + bankrollCode + "&bankCode=" + this.model.bankCode).then(({data}) => {
                        data.forEach((v) => {
                            this.branchCodeList.push({key: v.unionNo, value: v.bankName})
                        });
                    });

                }
            }
        },

        methods: {
            bankFilter(val) {
                return "$" + val;``
            },


            saveBank() {
                if (this.model.bankUnionNo == "") {
                    this.$vux.toast.show({
                        text: "请输入支行",
                        type: "cancel"
                    });
                    return
                }
                if (this.model.bankAccount == "" || (!/^\d{9,17}$/.test(this.model.bankAccount))) {
                    this.$vux.toast.show({
                        text: '请输入正确的银行卡账号',
                        type: "cancel"
                    })
                    return;
                }
                this.$root.showLoading = true;
                this.model.bankProvinceCode = this.addressCode[0];
                this.model.bankCityCode = this.addressCode[1];
                this.$http.post('api/auth/enterprise/banks', this.model)
                    .then(({data}) => {
                        this.$root.showLoading = false
                        if (data._code == 200) {
                            this.$router.push({path: "/enterprise/contacts"})
                        } else {
                            this.$vux.toast.show({
                                text: data._msg,
                                type: "cancel"
                            })
                        }
                    })
            },
            branchChangeEvent(newVal){

                this.model.bankProvinceCode = '';
                this.model.bankCityCode = '';
                let bankrollCode = this.addressCode[1];
                if (bankrollCode == undefined) {
                    this.branchCodeList = [];
                } else {
                    if (this.model.bankCode != newVal) {
                        this.branchCodeList = [];
                        this.$http.get("api/system/bank/union/numbers?bankrollCode=" + bankrollCode + "&bankCode=" + newVal).then(({data}) => {
                            data.forEach((v) => {
                                this.branchCodeList.push({key: v.unionNo, value: v.bankName})
                            });
                        });
                    }
                }

                this.model.bankCode = newVal;
                this.model.bankName = key2value(newVal, this.bankCodeList);
            },
            bankCodeChangeEvent(newVal){
                this.model.bankUnionNo = newVal;
                this.model.bankBranchName = key2value(newVal, this.branchCodeList);
            }
        }
    }

</script>
