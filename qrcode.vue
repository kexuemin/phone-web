<template>

    <div style="text-align:center;padding-top:15px;height:100%;background:#fff;">
        <img :src="model.qrcodeUrl" width="300" height="300">
    </div>


</template>


<script>
    export default {
        data()
        {
            return {
                model: {
                    qrcodeUrl: ""
                }
            }
        }
        ,
        mounted()
        {
            this.$http.get("api/auth/qrcodes",
                {headers: {'X-Auth-Token': 'cmVyZXJlcmVkZmQtZDI4YzVlODJhNTk1NDdlOWIxMjJmZmE1NzNlMDc3NTM='}}).then(({data}) => {
                this.model.qrcodeUrl = data.url;
            });
        }
    }
</script>
