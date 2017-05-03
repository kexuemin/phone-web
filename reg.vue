<style scoped>
    html, body {
        background: #fff;
        height: 100%;
    }

    .page-panel {
        margin: 15px 10px 0 10px;
    }

    .app-reg {
        /*padding: 15px;*/
        background-color: #fff;
        min-height: 100%;
        width: 100%;
    }

    .app-reg .reg-header {
        font-size: 22px;
        color: #475568;
        padding: 60px 5px;
        font-weight: bold;
    }

    .weui-label {
        width: 82px;
    }

    .weui-cells:before {
        border-top: 0;
    }

    .weui-cell:before {
        height: 0;
        top: 12px;
        border-top: 0;
    }

    .app-1px-b:after {
        height: 0;
        border-bottom: 0;
    }

    .weui-cell {
        padding: 0;
        height: 45px;
        line-height: 45px;
        border-bottom: 1px solid #d9d9d9;
    }

    .weui_cells_tips {
        padding: 20px 10px;
        text-align: left;
    }

    .tips-text {
        color: #217df0;
    }

    .mindai {
        margin: 30px 0 10px 0;
        text-align: center;
    }

    .app-btn-primary {
        border-radius: 5px;
    }

    .static {
        position: absolute;
        left: 10px;
        width: 16px;
        height: 16px;
        background: url(../../assets/img/select_btn.png) no-repeat;
        background-size: 100%;
    }

    .btn-area {
        margin-bottom: 3em;
    }

    .footer {
        width: 80%;
        margin: 0 auto;
        /*margin-top: 50px;
        text-align:center;*/
        background: #fff;
    }

    .img_icon {
        width: 50%;
        height: 30px;
        float: left;

    }

    .img_icon img {
        margin: 0 auto;
        width: 90px;
        height: 30px;
        display: inline-block;

    }

    .copyright {
        /*float: left;
        width: 100%;*/
        text-align: center;
        height: 30px;
        line-height: 30px;
        background: #fff;
        padding-top: 20px;
    }

    .weui-cells_checkbox .weui-icon-checked:before {
        font-size: 14px;
    }

    .weui-check {
        position: absolute;
        left: 0em;
        width: 30px;
        height: 50px;
        opacity: 0;
    }

    .weui-cells_checkbox .weui-cell__hd {
        padding-right: 0;
    }

    .weui-cells:after {
        border-bottom: 0;
    }

    .weui-cells_checkbox .weui-check:checked + .weui-icon-checked:before {
        color: #217DF0;
    }

    .weui-btn_primary:not(.weui-btn_disabled):active {
        background: #217DF0;
    }

    .clear {
        clear: both;
    }

    a {
        color: #475568;
    }

    .active {
        width: 16px;
        height: 16px;
        background: url(../../assets/img/select_active.png) no-repeat;
        background-size: 100%;
    }

    .agree-btn {
        position: absolute;
        left: 28px;
        top: 8px;
    }
    #about{
        position: absolute;
        left: 0;
        top: 0;
        background: #fff;
        /*height: 100%;*/
        z-index: 10;
    }

    .agree-text{
    padding: 10px;
    font-size: 12px;
  margin-bottom: 30px;
}
.um_tabbar{
    width:90px;
    margin: 0 auto;
    margin-bottom: 50px;
}
.um_tabbar_btn{
    width:100px;
    height: 30px;
    line-height: 30px;
    margin: 0 auto;
    background: #217DF0;
    border: 0;
    text-align: center;

}
.um_tabbar_btn a{
    color: #fff;
}
.app-con{
    padding:15px;
    background: #fff;
}
</style>

<template>
    <div class="app-reg">
        <div class="app-con">
            <div class="reg-header">
                只需4步，简单申请授信
            </div>
            <div class="weui-cells weui-cells_form app-1px-b page-panel">
                <!-- <div class="weui-cell">
                    <div class="weui-cell__hd"><label class="weui-label" >姓名</label></div>
                    <div class="weui-cell__bd">
                        <input class="weui-input" type="text" placeholder="请输入姓名" v-model="model.realname">
                    </div>
                </div> -->
                <div class="weui-cell weui-cell_vcode">
                    <div class="weui-cell__hd">
                        <label class="weui-label">法人手机号</label>
                    </div>
                    <div class="weui-cell__bd">
                        <input class="weui-input" type="tel"
                               v-model="model.phoneNo" placeholder="请输入手机号" maxlength="11">
                    </div>

                </div>
                <div class="weui-cell">
                    <div class="weui-cell__hd">
                        <label class="weui-label">验证码</label>
                    </div>
                    <div class="weui-cell__bd">
                        <input class="weui-input" type="text" v-model="model.valid" placeholder="请输入验证码">
                    </div>
                    <div class="weui-cell__ft">
                        <button class="weui-vcode-btn" v-if="validSecond == 0" @click="sendValid" style="color:#217DF0;">
                            获取验证码
                        </button>
                        <button class="weui-vcode-btn" style="color:#217DF0;" v-if="validSecond > 0">{{validSecond}}s

                        </button>
                    </div>
                </div>

            </div>
            <div class="weui-cells weui-cells_checkbox">
                <label class="weui-cell weui-check__label" style="border-bottom: 0;" for="s11">
                    <!-- <div class="weui-cell__hd">
                        <input type="checkbox" class="weui-check" name="checkbox1" id="s11" checked="checked">
                        <i class="weui-icon-checked"></i>
                    </div> -->
                    <div class="weui-cell__bd">

                        <div class="static" v-bind:class="{ active: isActive}" @click="isActive = !isActive"
                             v-model="isActive"></div>
                        <div class="agree-btn">同意
                            <router-link :to="{path:'/enterprise/reg#about'}" v-on:click.native="ok = !ok">《信息授权协议》</router-link>
                        </div>
                    </div>
                </label>
            </div>
            <p class="mindai">授信额度由民贷天下提供</a></p>
            <div id="about" v-if="ok">
               <div class="agree-text">
                <br>因申请办理信用优惠购机业务，特在此向广州秒钛科技有限公司不可撤销地同意和授权如下：

                <br>1、  知晓并同意广州秒钛科技有限公司向深圳前海征信中心股份有限公司采集、查询、使用、报送本人的信息，含到期未及时缴纳手机套餐使用等不良信息。

                <br>2、  知晓并同意上海资信征信有限公司和征信中心将本人在广州秒钛科技有限公司产生的信用信息纳入由上海资信征信有限公司建设的网络金融征信系统（NFCS）和征信中心运营的金融信用信息基础数据库，用于相关法律、法规、规章和规范性文件规定的用途；同意广州秒钛科技有限公司向上海资信征信有限公司查询本人在NFCS网络金融征信系统中的个人信用信息，及通过上海资信征信有限公司向征信中心查询本人的个人信用信息。

                <br>3、  知晓并同意芝麻信用有权基于提供征信服务的需要向合法保存有本人信息的机构采集本人信息（包括由广州秒钛科技有限公司有权将本人在使用其服务过程中提交或产生的信息提供给芝麻信用），用于验证本人信息的真实性及提供征信服务使用。本人授权芝麻信用，可根据优钱的查询指令，向其提供相关信息的真实性判断结果及本人的信用信息，用以交易决策使用。

                <br>4、  知晓并同意在注册帐号或使用本服务的过程中，提供并授权广州秒钛科技有限公司获取以下信息：本人手机号码；本人所在的地理位置信息；授权广州秒钛科技有限公司访问本人手机通讯录等。授权广州秒钛科技有限公司读取本人手机短信的相关信息。

                <br>5、知晓并同意开通刷脸服务后，广州秒钛科技有限公司采集并保存借款人脸部图片。

                <br>以上信息的授权限于办理本业务以及因本业务发生的相关业务，包括保险业务中的投保、理赔、追偿等。不管本业务申请是否获批，该授权均持续有效。
                就授权的范围内申请人信息的采集、提供、传输、处理、披露，将不视为对申请人任何权利和利益的侵犯，申请人不追究甲方和征信机构的任何责任。
                </div>
                <div class="um_tabbar">
                    <div class="um_tabbar_item">
                        <!-- <button class="um_tabbar_btn_primary um_tabbar_btn" v-link="{path:'/user/edit'}">同意授权</button>     -->
                        <p class="um_tabbar_btn_primary um_tabbar_btn"><router-link :to="{path:'/enterprise/reg'}"  v-on:click.native="ok = !ok">返回</router-link>

                        </p>    
                    </div>
                </div>
            </div>
            <div class="btn-area">
                <button class="weui-btn weui-btn_primary app-btn-primary" @click="saveUser">下一步</button>
            </div>
            <div class="footer">
                <div class="img_icon">
                    <img src="../../assets/img/footer_left.png">
                </div>
                <div class="img_icon">
                    <img src="../../assets/img/footer_right.png">
                </div>
                <div class="clear"></div>
            </div>
            <div class="copyright">由秒钛坊提供技术支持</div>
        </div>
    </div>
</template>

<script>


    export default {

        mounted(){
            this.$http.get("api/auth").then(({data}) => {
                if(data && "REGISTER" == data.status) {
                    this.$router.push({path: "/enterprise/idcard"});
                }
            });
        },
        data() {
            return {
                model: {phoneNo: "", valid: "", count: 0, capitalEnterpriseId:"d28c5e82a59547e9b782ffa573e07754", productId:"d28c5e82a59547e9b122ffa573e01713"},
                showLoading: false,
                showSuccess: false,
                showError: false,
                validSecond: 0,
                errorMsg: "",
                isActive: true,
                hasError: true,
                ok:false
            }
        },
        methods: {
            saveUser() {
                if (this.model.phoneNo == "" || (!/^1[3,5,8,7]\d{9}$/.test(this.model.phoneNo) )) {
                    this.$vux.toast.show({
                        text: '请输入正确的手机号',
                        type: "cancel"
                    });
                    return;
                }
                if (!this.model.valid) {
                    this.$vux.toast.show({
                        text: "请输入验证码",
                        type: "cancel"
                    })
                    return
                } else if (this.isActive == false) {
                    this.$vux.toast.show({
                        text: "请选择同意授权协议",
                        type: "cancel"
                    });
                    return;
                }
                this.$root.showLoading = true;
                this.$http.post('api/auth/reg', this.model)
                    .then(({data}) => {
                        this.$root.showLoading = false;
                        if (data._code && data._code == 200) {
                            this.$vux.toast.show({
                                text: "验证成功",
                                type: "success"
                            })
                            this.$router.push({path: "/enterprise/idcard"})
                        } else {
                            this.$vux.toast.show({
                                text: data._msg || "验证码发送失败",
                                type: "cancel"
                            })
                        }
                    })
            },
            sendValid() {

                if (this.model.phoneNo == "" || (!/^1[3,5,8,7]\d{9}$/.test(this.model.phoneNo) )) {
                    this.$vux.toast.show({
                        text: '请输入正确的手机号',
                        type: "cancel"
                    });
                    return;
                }
                this.validSecond = 60;
                this.$http.post("api/auth/codes", {
                    phoneNo: this.model.phoneNo
                }).then(({data}) => {
                    this.model.count = data.params || 0
                    if (data._code == 200) {
                        let interval = setInterval(() => {
                            if (this.validSecond < 1) {
                                clearInterval(interval)
                                this.validSecond = 0
                            } else {
                                this.validSecond = this.validSecond - 1
                            }
                        }, 1000);
                    } else {
                        this.validSecond = 0
                        this.$vux.toast.show({
                            text: data._msg || "验证码发送失败",
                            type: "cancel"
                        })
                    }
                });
            }
        }
    }

</script>
