<template>
  <div class="Detail">
    <h3 class="companyName">
      <img src="../../static/images/back.png" style="width:30px;float:left" @click="back" />
      <span class="text">{{listItem.title}}</span>
    </h3>
    <div class="companyIntroduce" v-html="listItem.info"></div>
    <div class="detailMessage" v-if="listItem.mobile1||listItem.siteurl||listItem.place">
      <div class="phone" v-if="listItem.mobile1">联系方式:{{listItem.mobile1}}</div>
      <div class="website" v-if="listItem.siteurl">网址:{{listItem.siteurl}}</div>
      <div class="address" v-if="listItem.place">地址:{{listItem.place}}</div>
    </div>
  </div>
</template>
<script>
export default {
  name: "Detail",
  data() {
    return {
      listItem: {}
    };
  },
  created() {
    let id = this.$route.query.id;
    this.http.get("amouse.index.getDetail", { id }).then(res => {
      this.listItem = res.data.detail;
    });
  },
  methods: {
    back() {
      this.$router.go(-1);
    },
    // see(e){
    //   window.location.href=e
    // }
  }
};
</script>
<style scoped>
.Detail {
  padding: 10px;
}
.Detail .companyName {
  text-align: center;
  font-size: 18px;
  padding: 10px 0;
  color: #333;
  font-weight: 600;
  display: flex;
  align-items: center;
}
.Detail .companyName span {
  margin: 0 auto;
}
.companyIntroduce {
  font-size: 30rpx;
  text-align: justify;
  color:#333;
}
.detailMessage {
  margin: 40px auto;
  font-weight: 600;
  padding: 10px 0;
  color: #737373;
  border: 2px dotted #ebebeb;
  text-align: center;
  font-size: 14px;
}

.detailMessage div {
  margin: 5px 0;
  font-weight: normal;
}
</style>