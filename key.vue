<style scoped>
html,body{
  background: #fff;
  height: 100%;
}
.page-panel{
    margin: 15px 10px 0 10px;
}
.app-reg{padding:15px;background-color: #fff;height: 100%;padding-bottom: 50px;}
.app-reg .reg-header{
  font-size: 22px;
  color: #475568;
  padding:60px 5px;
  font-weight:bold;
}
.weui-label{
    width: 82px;
}
.weui-cells:before{
    border-top:0;
}
.weui-cell:before{
    height:0;
    top: 12px;
    border-top:0;
}
.app-1px-b:after{
    height:0;
    border-bottom:0;
}
.weui-cell{
    padding:0;
    height: 45px;
    line-height: 45px;
    border-bottom: 1px solid #d9d9d9;
}
.weui_cells_tips{
    padding: 20px 10px;
    text-align: left;
}
.tips-text{
    color: #217df0;
}
.mindai{
    margin: 30px 0 10px 0 ;
    text-align: center;
}
.app-btn-primary{
    border-radius: 5px;
}
.static{
  position: absolute;
  left:10px;
  width: 16px;
  height: 16px;
  background:url(../../assets/img/select_btn.png) no-repeat;
  background-size: 100%;
}
.img_icon{
    width:50%;
    height:30px;
    float: left;
    
}
.img_icon img{
    margin: 0 auto;
    width:90px;
    height:30px;
    display:inline-block;

}
.copyright-bottom{
  float: left;
  width: 100%;
  text-align: left;
  height: 30px;
  line-height: 30px;
  background: #fff;
  padding-top:20px;
}

.weui-cells_checkbox .weui-icon-checked:before{
  font-size: 14px;
}
.weui-check {
    position: absolute;
    left: 0em;
    width: 30px;
    height: 50px;
    opacity: 0;
}
.weui-cells_checkbox .weui-cell__hd{
  padding-right: 0;
}
.weui-cells:after{
  border-bottom:0;
}
.weui-cells_checkbox .weui-check:checked + .weui-icon-checked:before{
  color: #217DF0;
}
.weui-btn_primary:not(.weui-btn_disabled):active{
  background: #217DF0;
}
.clear{
  clear: both;
}
a{
  color: #475568;
}
.active{
  width: 16px;
  height: 16px;
  background:url(../../assets/img/select_active.png) no-repeat;
  background-size: 100%;
}
.agree-btn{
  position: absolute;
  left: 28px;
  top: 8px;
}
.btn-area{
  margin-top: 50px;
  margin-bottom: 10px;
}
.weui-key{
  display: inline-block;
  width: 20px;
  height: 20px;
  background:url(../../assets/img/symbols-icon.png) no-repeat;
  background-size: 100%;
  margin:12px 15px 0 0;
}
.weui-key2{
  display: inline-block;
  width: 20px;
  height: 20px;
  background:url(../../assets/img/symbols-icon2.png) no-repeat;
  background-size: 100%;
  margin:12px 15px 0 0;
}
</style>

<template>
<div class="app-reg">
      <div class="reg-header">
            设置交易密码
      </div>
         <div class="weui-cells weui-cells_form app-1px-b page-panel">
            <div class="weui-cell weui-cell_vcode">
                <div class="weui-cell__hd">
                    <label class="weui-key"></label>
                </div>
                <div class="weui-cell__bd">
                    <input class="weui-input" type="password"
                     v-model="model.paymentPassword" placeholder="请输6位数的密码" maxlength="6" autofocus="autofocus">                
                </div>
               
            </div>

        </div>
        <div class="weui-cells weui-cells_form app-1px-b page-panel">
            <div class="weui-cell weui-cell_vcode">
                <div class="weui-cell__hd">
                    <label class="weui-key2"></label>
                </div>
                <div class="weui-cell__bd">
                    <input class="weui-input" type="password"
                     v-model="checkedPassword" placeholder="请再次输入密码" maxlength="6" minlength="6">
                </div>
               
            </div>

        </div>
        <!-- <p class="mindai">授信额度由民贷天下提供</a></p> -->

     <div class="btn-area"><button class="weui-btn weui-btn_primary app-btn-primary" @click="savePaymentPassword">下一步</button></div>
      <!-- <div class="footer">
         <div class="img_icon">
              <img src="../../assets/img/footer_left.png">
          </div>
           <div class="img_icon">
              <img  src="../../assets/img/footer_right.png">
          </div>
          <div class="clear"></div>
      </div> -->
      <div class="copyright-bottom">交易密码用于每次贷款申请时确认的电子凭证，用于签署具有
法律效力的电子合同，以保障借贷双方的权益。
 </div>
</div>
</template>

<script>


export default {

    created(){
    },
    data() {
        return {
            model: {phoneNokey:"",phoneKey:"",valid:"",count:0},
            showLoading: false,
            showSuccess: false,
            showError: false,
            validSecond: 0,
            checkedPassword:"",
            errorMsg: "" ,
            isActive: false,
            hasError: true
        }
    },
    methods: {
        savePaymentPassword() {
            if (this.model.paymentPassword == "" || (!/^[0-9]\d{0,5}$/.test(this.model.paymentPassword) ) || (this.model.paymentPassword.length!=6))
            {
                this.$vux.toast.show({
                    text: '请输入6位数字密码',
                    type:"cancel"
                })
                return;
            }
            if (this.checkedPassword != this.model.paymentPassword) {
                this.$vux.toast.show({
                    text: '两次输入密码不一致',
                    type:"cancel"
                })
                return;
            }
            this.$root.showLoading = true
            this.$http.post('api/auth/enterprise/paymentpassword', this.model)
                .then(({data}) => {
                    this.$root.showLoading = false;
                    if (data._code && data._code == 200) {
                        this.$router.replace({path:"/enterprise/last"})
                    }else {
                        this.$vux.toast.show({
                         text: data._msg||"设置交易密码失败",
                         type:"cancel"
                        })
                    }
                });
            }

    }
}

</script>
