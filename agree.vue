<style scoped>

.agree-header {
    padding-top: 20px;
    font-weight: bold;
    font-size: 18px;
    text-align: center;
    color: #222;
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
</style>

<template>

<div>
    <div class="agree-header">
        <!--<img src="../../assets/img/reg-logo.png" class="logo">-->
        	征信授权协议
    </div>
    <div class="agree-text">
<br>因申请办理信用优惠购机业务，特在此向广州秒钛科技有限公司不可撤销地同意和授权如下：

<br>1、	知晓并同意广州秒钛科技有限公司向深圳前海征信中心股份有限公司采集、查询、使用、报送本人的信息，含到期未及时缴纳手机套餐使用等不良信息。

<br>2、	知晓并同意上海资信征信有限公司和征信中心将本人在广州秒钛科技有限公司产生的信用信息纳入由上海资信征信有限公司建设的网络金融征信系统（NFCS）和征信中心运营的金融信用信息基础数据库，用于相关法律、法规、规章和规范性文件规定的用途；同意广州秒钛科技有限公司向上海资信征信有限公司查询本人在NFCS网络金融征信系统中的个人信用信息，及通过上海资信征信有限公司向征信中心查询本人的个人信用信息。

<br>3、	知晓并同意芝麻信用有权基于提供征信服务的需要向合法保存有本人信息的机构采集本人信息（包括由广州秒钛科技有限公司有权将本人在使用其服务过程中提交或产生的信息提供给芝麻信用），用于验证本人信息的真实性及提供征信服务使用。本人授权芝麻信用，可根据优钱的查询指令，向其提供相关信息的真实性判断结果及本人的信用信息，用以交易决策使用。

<br>4、	知晓并同意在注册帐号或使用本服务的过程中，提供并授权广州秒钛科技有限公司获取以下信息：本人手机号码；本人所在的地理位置信息；授权广州秒钛科技有限公司访问本人手机通讯录等。授权广州秒钛科技有限公司读取本人手机短信的相关信息。

<br>5、知晓并同意开通刷脸服务后，广州秒钛科技有限公司采集并保存借款人脸部图片。

<br>以上信息的授权限于办理本业务以及因本业务发生的相关业务，包括保险业务中的投保、理赔、追偿等。不管本业务申请是否获批，该授权均持续有效。
就授权的范围内申请人信息的采集、提供、传输、处理、披露，将不视为对申请人任何权利和利益的侵犯，申请人不追究甲方和征信机构的任何责任。
</div>
    <div class="um_tabbar">
        <div class="um_tabbar_item">
            <!-- <button class="um_tabbar_btn_primary um_tabbar_btn" v-link="{path:'/user/edit'}">同意授权</button>     -->
            <p class="um_tabbar_btn_primary um_tabbar_btn"><router-link :to="{path:'/enterprise/reg'}">返回</router-link>

            </p>    
        </div>
    </div>
</div>
</template>
