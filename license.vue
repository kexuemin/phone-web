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
        z-index: 2;
    }
    .take-pic img.uploadPicture{
        max-width: 200px;
    }
    .header-step {
        padding: 10px 15px;
    }

    .page-panel {
        padding: 15px 10px 0 10px;
        margin-top:0;
    }

    .title {
        margin: 0px 18px;
        margin-top: 15px;
        color: #fc8928;
    }

    .app-btn-primary {
        border-radius: 5px;
        background: #217DF0;
        color: #fff;
    }

    .page-panel p {
        margin: 0 8px;
    }

    .take-pic strong {
        font-size: 14px;
        top: 60%;
    }

    .vux-checker-box {
        margin-top: 20px;
        /*margin-bottom: 10px;*/
    }

    .demo2-item {
        /*margin-right: 3px;
        margin-left: 32px;*/
        float: left;
        width: 50%;
        height: 50%;
        border-bottom: 1px solid #d9d9d9;
        display: inline-block;
        /*border-radius: 50%;*/
        height: 40px;
        line-height: 40px;
        text-align: center;
    }

    .demo2-item-selected {
    /*border-color: #217DF0;*/
    border-bottom: 2px solid #217DF0;
    color: #217DF0;
    }
    .line-y{
    display: block;
    height: 24px;
    width: 1px;
    background: #d9d9d9;
    position: absolute;
    top: 8px;
    left: 50%;
    }
    .checker{
    position: relative;
    height: 40px;
    line-height: 40px;
    background: #fff;

    }
</style>

<template>
    <div class="page">
        <div class="header">
            <!-- <app-step :step="1"></app-step> -->
            <div class="header-step">
                <img src="../../assets/img/flow/step2.png" style="width:100%;"/>
            </div>

        </div>
        <!-- <p class="title">请注意平台授信必须由法人本人提出申请</p> -->
        <checker v-model="model.integrated" default-item-class="demo2-item" selected-item-class="demo2-item-selected" class="checker">
            <checker-item value="Y">三证合一</checker-item>
            <span class="line-y"></span>


            <checker-item value="N">未三证合一</checker-item>
            <!-- <span>未三证合一</span> -->


        </checker>
        <div class="page-panel">
            <p>请按图示上传您的资料</p>
            <div>
                <ul class="pic-up">
                    <li class="row">
                        <div class="exp-pic">
                            <img src="../../assets/img/yingye1.png" alt=""/>
                            <!-- <span class='exp-pic-tip'>查看示例大图</span> -->
                        </div>
                        <div class="take-pic" @click="uploadPhoto('licensePic')">
                            <strong class="tip-text">上传营业执照</strong>
                            <img class="uploadPicture" v-if="model.licensePic" :src="model.licensePic"/>
                            <img v-else src="../../assets/img/upload-file.png">
                        </div>
                    </li>

                    <div v-if="model.integrated == 'N'">
                        <li class="row">
                            <div class="exp-pic">
                                <img src="../../assets/img/yingye2.png" alt=""/>
                                <!-- <span class='exp-pic-tip'>查看示例大图</span> -->
                            </div>
                            <div class="take-pic" @click="uploadPhoto('taxPic')">
                                <strong class="tip-text">上传税务登记证</strong>
                                <img class="uploadPicture" v-if="model.taxPic" :src="model.taxPic"/>
                                <img v-else src="../../assets/img/upload-file.png">
                            </div>
                        </li>
                        <li class="row">
                            <div class="exp-pic">
                                <img src="../../assets/img/yingye3.png" alt=""/>
                                <!-- <span class='exp-pic-tip'>查看示例大图</span> -->
                            </div>
                            <div class="take-pic" @click="uploadPhoto('orgCodePic')">
                                <strong class="tip-text">上传组织机构代码证</strong>
                                <img class="uploadPicture" v-if="model.orgCodePic" :src="model.orgCodePic"/>
                                <img v-else src="../../assets/img/upload-file.png">
                            </div>
                        </li>
                    </div>
                </ul>

            </div>

        </div>


        <div class="btn-area" style="margin:20px 15px;">
            <button class="weui-btn app-btn-primary" @click="uploadPhotos">下一步</button>
        </div>
    </div>
</template>

<script>
    import {Badge, CheckerItem, Checker} from '../../vux/index'
    export default {
        components: {
            CheckerItem, Checker
        },
        data() {
            return {
                model: {
                    licensePic: "",
                    taxPic: "",
                    orgCodePic: "",
                    integrated:"Y"
                },
                upload: {
                    showUpload: true
                }
            }
        },
        mounted(){
            this.$http.get("api/auth").then(({data}) => {
                let bankModel = {};
                Object.assign(bankModel, this.model, data);
                this.model = bankModel;
            });
        },
        methods: {
            uploadPhotos() {
                if (this.model.integrated == "") {
                    this.$vux.toast.show({
                        text: "请选择是否三证合一",
                        type: "cancel"
                    });
                    return;
                }

                if (this.model.integrated == 'Y' && !this.model.licensePic) {
                    this.$vux.toast.show({
                        text: "请上传照片信息",
                        type: "cancel"
                    });
                    return;
                }
                if ((this.model.integrated == 'N' && !this.model.licensePic) || (this.model.integrated == 'N' && !this.model.taxPic) || (this.model.integrated == 'N' && !this.model.orgCodePic)) {
                    this.$vux.toast.show({
                        text: "请上传照片信息",
                        type: "cancel"
                    });
                    return;
                }
                this.showLoading = true;
                this.$http.post('api/auth/identification/photos', this.model)
                    .then(({data}) => {
                        this.showLoading = false
                        if (data._code == 200) {
                            this.$router.push({path: "/enterprise/information"})
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
                        this.$vux.loading.show({text: '文件上传中...'});
                        wx.uploadImage({
                            localId: res.localIds[0], // 需要上传的图片的本地ID，由chooseImage接口获得
                            isShowProgressTips: 0, // 默认为1，显示进度提示
                            success: (res) => {
                                this.$http.post('api/wechat/upload', {mediaId: res.serverId}).then(({data}) => {
                                    this.$vux.loading.hide();
                                    this.model[type] = data.url
                                });
                            }
                        });
                    }
                })
            },
            previewImage (url){
                wx.previewImage({
                    current: url,
                    urls: [
                        'http://youqian-static.oss-cn-hangzhou.aliyuncs.com/web/img/card_face.png',
                        'http://youqian-static.oss-cn-hangzhou.aliyuncs.com/web/img/card_side.png',
                        'http://youqian-static.oss-cn-hangzhou.aliyuncs.com/app/img/page5.jpg'
                    ]
                })
            }
            // uploadCard (){
            //     if ((model.integrated == 'Y' && this.model.licensePic) ||
            //         (model.integrated == 'N' && this.model.licensePic && this.model.taxPic && this.model.orgCodePic)) {

            //     } else {
            //         this.$vux.toast.show({
            //             text: "请上传照片信息",
            //             type: "cancel"
            //         });
            //         return;
            //     }
            // }
        }
    }
</script>
