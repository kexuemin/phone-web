<style scoped>
    .header {
        background: #fff;
    }

    .pic-up {
        width: 95%;
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
        top: 5px;
        width: 100%;
        /*max-width: 200px;*/
        z-index: 2;
    }
    .take-pic img.uploadPicture{
        max-width: 200px;
    }
    .header-step {
        padding: 10px 15px;
    }

    .page {
        background: #F2F3F7;
    }

    .page-panel {
        margin: 0;
    }

    .title {
        padding: 0px 18px;
        height: 40px;
        line-height: 40px;
        color: #fc8928;
        background: #F2F3F7;
        font-size: .95em;
    }

    .app-btn-primary {
        border-radius: 5px;
        background: #217DF0;
        color: #fff;
    }

    .page-panel p {
        margin: 0 8px;
        padding-top: 10px;
    }

    .page-con {
        padding: 2px 10px 0 10px;
        background: #fff;
    }

    .weui-cell:before {
        /*border-top: 0;*/
    }

    .weui-cells {
        margin-top: 20px;
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
</style>

<template>
    <div class="page">
        <div class="header">
            <!-- <app-step :step="1"></app-step> -->
            <div class="header-step">
                <img src="../../assets/img/flow/step1.png" style="width:100%;"/>
            </div>
        </div>
        <div class="page-panel" style="background:#F2F3F7;" v-if="step == 1">
            <div class="title">请注意平台授信必须由法人本人提出申请 </div>

            <div class="page-con">
                <p>请按图示上传您的资料</p>
                <ul class="pic-up">
                    <li class="row">
                        <div class="exp-pic"
                             @click="previewImage('http://youqian-static.oss-cn-hangzhou.aliyuncs.com/web/img/card_face.png')">
                            <img src="../../assets/img/card_side_small.png" alt=""/>
                            <span class='exp-pic-tip'>查看示例大图</span>
                        </div>
                        <div class="take-pic" @click="uploadPhoto('idcardFrontPic')">
                            <strong class="tip-text">身份证 正面照</strong>
                            <img class="uploadPicture" v-if="model.idcardFrontPic" :src="model.idcardFrontPic"/>
                            <img v-else src="../../assets/img/upload-file.png">
                        </div>
                    </li>
                    <li class="row">
                        <div class="exp-pic"
                             @click="previewImage('http://youqian-static.oss-cn-hangzhou.aliyuncs.com/web/img/card_side.png')">
                            <img src="../../assets/img/card_face_small.png" alt=""/>
                            <span class='exp-pic-tip'>查看示例大图</span>
                        </div>
                        <div class="take-pic" @click="uploadPhoto('idcardBackPic')">
                            <strong class="tip-text">身份证 反面照</strong>
                            <img class="uploadPicture" v-if="model.idcardBackPic" :src="model.idcardBackPic"/>
                            <img v-else src="../../assets/img/upload-file.png">
                        </div>
                    </li>
                    <li class="row">
                        <div class="exp-pic"
                             @click="previewImage('http://youqian-static.oss-cn-hangzhou.aliyuncs.com/app/img/page5.jpg')">
                            <img src="http://youqian-static.oss-cn-hangzhou.aliyuncs.com/app/img/page5.png" alt=""/>
                        </div>
                        <div class="take-pic" @click="uploadPhoto('idcardSelfPic')">
                            <strong class="tip-text">正面手持照</strong>
                            <img class="uploadPicture" v-if="model.idcardSelfPic" :src="model.idcardSelfPic"/>
                            <img v-else src="../../assets/img/upload-file.png">
                        </div>
                    </li>
                </ul>
            </div>
            <div class="btn-area" style="margin:20px 15px;background:#F2F3F7;">
                <button class="weui-btn app-btn-primary" @click="uploadCard">下一步</button>
            </div>
        </div>

        <div class="" v-if="step == 2">
            <!-- <div class="weui-cells_title"></div> -->
            <group class="weui-cells_form page-panel">
                <div class="weui-cell">
                    <div class="weui-cell_hd">
                        <label class="weui-label">法人姓名</label>
                    </div>
                    <div class="weui-cell_bd weui-cell_primary">
                        <input class="weui-input" type="text" v-input-change="model.legalPersonName"
                               placeholder="请输入真实姓名"
                               v-model="model.legalPersonName"/>
                    </div>
                </div>
                <div class="weui-cell">
                    <div class="weui-cell_hd">
                        <label class="weui-label">身份证号码</label>
                    </div>
                    <div class="weui-cell_bd weui-cell_primary">
                        <input class="weui-input" type="text" v-input-change="model.legalPersonIdcard"
                               placeholder="请输入身份证号码"
                               v-model="model.legalPersonIdcard"/>
                    </div>
                </div>
            </group>

            <group class="weui-cells_form">
                <div class="weui-cell">
                    <div class="weui-cell_hd">
                        <label class="weui-label">储蓄卡号</label>
                    </div>
                    <div class="weui-cell__bd weui-cell_primary">
                        <input class="weui-input" type="tel" v-input-change="model.legalPersonBankAccount"
                               placeholder="请输入储蓄卡号" v-model="model.legalPersonBankAccount"/>
                    </div>
                </div>

                <selector title="开户行" placeholder="请选择开户行" :options="bankCodeList" @on-change="branchChangeEvent"
                              :value="model.legalPersonBankCode"></selector>

                <div class="weui-cell">
                    <div class="weui-cell_hd">
                        <label class="weui-label">手机号码</label>
                    </div>
                    <div class="weui-cell__bd weui-cell_primary">
                        <input class="weui-input" type="tel" placeholder="请输入银行预留手机号"
                               v-input-change="model.legalPersonBankPhone" v-model="model.legalPersonBankPhone"/>
                    </div>
                </div>
            </group>
            <div title="请按图示要求上传您的银行卡照片">
                <ul class="pic-up">
                    <li class="row">
                        <div class="exp-pic"
                             @click="previewImage('http://sectech-static.oss-cn-hangzhou.aliyuncs.com/wechat/img/bank.png')">
                            <img src="../../assets/img/bank.png" alt=""/>
                            <span class='exp-pic-tip'>查看示例大图</span>
                        </div>
                        <div class="take-pic" @click="uploadPhoto('legalPersonBankPic')">
                            <strong class="tip-text">银行卡 正面照</strong>
                            <img class="uploadPicture" v-if="model.legalPersonBankPic" :src="model.legalPersonBankPic"/>
                            <img v-else src="../../assets/img/upload-file.png">
                        </div>
                    </li>
                </ul>
            </div>

            <div class="btn-area" style="margin:20px 15px;background:#F2F3F7;">
                <button class="weui-btn app-btn-primary" @click="saveUser">下一步</button>
            </div>
        </div>
    </div>
</template>

<script>
    import AppStep from '../../components/app-step'
    import {Badge, Selector} from '../../vux/index'
    import wx from 'weixin-js-sdk'
    import {luhmCheck} from '../../utils/bankCheckUtils'

    export default {
        components: {
            AppStep, Selector
        },
        data() {
            return {
                model: {
                    status: '',
                    legalPersonName: "",
                    legalPersonIdcard: "",
                    legalPersonBankAccount: "",
                    legalPersonBankCode: "",
                    legalPersonBankPhone: "",
                    legalPersonBankPic:"",
                    idcardFrontPic: "",
                    idcardBackPic: "",
                    idcardSelfPic: ""
                },
                upload: {
                    showUpload: true
                },
                cardOrc: {
                    idcardFrontPic: "",
                    idcardBackPic: ""
                },
                bankCodeList: [],
                step: 1
            }
        },
        mounted(){
            this.$http.get("api/system/dics?type=bankInfo&status=Y").then(({data}) => {
                    data.forEach((v) => {
                        this.bankCodeList.push({key: v.value, value: v.name})
                    });

                    this.$http.get("api/auth/extensions").then(({data}) => {
                        let bankModel = {};
                        Object.assign(bankModel, this.model, data);
                        this.model = bankModel;
                    });
                }
            );
        },
        methods: {
            saveUser() {

                if (this.model.legalPersonName == "" || (!/^[\u4e00-\u9fa5]+$/.test(this.model.legalPersonName) )) {
                    this.$vux.toast.show({
                        text: '请输入中文姓名',
                        type: "cancel"
                    })
                    return;
                } else if (this.model.legalPersonIdcard == "" || (!/(^\d{15}$)|(^\d{17}([0-9]|X)$)/.test(this.model.legalPersonIdcard) )) {
                    this.$vux.toast.show({
                        text: '请输入正确的身份证号码',
                        type: "cancel"
                    })
                    return;
                }else if(this.model.legalPersonBankAccount=="" || !luhmCheck(this.model.legalPersonBankAccount)){
                    this.$vux.toast.show({
                        text: '请输入正确的银行卡账号',
                        type: "cancel"
                    })
                    return;
                }else if (this.model.legalPersonBankCode == "") {
                    this.$vux.toast.show({
                        text: "请选择开户行",
                        type: "cancel"
                    });
                    return
                } else if (this.model.legalPersonBankPhone == "" || (!/^1[3,5,8,7]\d{9}$/.test(this.model.legalPersonBankPhone) )) {
                    this.$vux.toast.show({
                        text: '请输入正确的手机号',
                        type: "cancel"
                    });
                    return;
                }
                else  if (!this.model.legalPersonBankPic) {
                    this.$vux.toast.show({
                        text: "请上传照片信息",
                        type: "cancel"
                    });
                    return
                } 

                this.showLoading = true;
                this.$http.post('api/auth/legal/names', this.model)
                    .then(({data}) => {
                        this.showLoading = false;
                        if (data._code == 200) {
                            this.$router.push({path: "/enterprise/license"})
                        } else {
                            this.$vux.toast.show({
                                text: data._msg,
                                type: "cancel"
                            })
                        }
                    })

            },
            uploadPhoto(type) {
                wx.chooseImage({
                    count: 1, // 默认9
                    sizeType: ['compressed'], // 可以指定是原图还是压缩图，默认二者都有
                    sourceType: ['camera'], // 可以指定来源是相册还是相机，默认二者都有
                    success: (res) => {
                        this.$vux.loading.show({text: '文件上传中...'})
                        wx.uploadImage({
                            localId: res.localIds[0], // 需要上传的图片的本地ID，由chooseImage接口获得
                            isShowProgressTips: 0, // 默认为1，显示进度提示
                            success: (res) => {
                                this.$http.post('api/wechat/upload', {mediaId: res.serverId}).then(({data}) => {
                                    this.$vux.loading.hide()
                                    this.model[type] = data.url
                                    var uploadOcr = {}
                                    uploadOcr[type] = data.id
                                    if ("idcardFrontPic" == type && data.url) {
                                        this.$http.post("api/auth/idcardocr", {cardPhoto: data.url}).then(({data}) => {
                                            if (data.outputStream.face.name && !this.model.legalPersonName) {
                                                this.model.legalPersonName = data.outputStream.face.name
                                            }
                                            if (data.outputStream.face.num && !this.model.legalPersonIdcard) {
                                                this.model.legalPersonIdcard = data.outputStream.face.num
                                            }
                                        })
                                    }
                                })
                            }
                        })
                    }
                })
            },
            previewImage (url){
                wx.previewImage({
                    current: url,
                    urls: [
                        'http://youqian-static.oss-cn-hangzhou.aliyuncs.com/web/img/card_face.png',
                        'http://youqian-static.oss-cn-hangzhou.aliyuncs.com/web/img/card_side.png',
                        'http://youqian-static.oss-cn-hangzhou.aliyuncs.com/app/img/page5.jpg',
                        'http://sectech-static.oss-cn-hangzhou.aliyuncs.com/wechat/img/bank.png'
                    ]
                })
            },
            uploadCard (){
                if (this.model.idcardFrontPic && this.model.idcardBackPic && this.model.idcardSelfPic) {
                    this.step = 2
                } else {
                    this.$vux.toast.show({
                        text: "请上传照片信息",
                        type: "cancel"
                    });
                    return
                }
            },
            branchChangeEvent(newVal){
                this.model.legalPersonBankCode = newVal;
            }
        }
    }
</script>
