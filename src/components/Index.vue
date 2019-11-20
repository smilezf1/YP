<template>
  <div class="Index">
    <div class="left classify" style="height:100%">
      <router-link
        v-for="(v,index) in listNav"
        v-bind:key="v.id"
        to="/"
        @click.native="switchMenu(index,v.id)"
        :class="{isActive:index==isActive}"
      >
        <img :src="v.thumb" style="width:35px;border-radius:3px;" />
        <span class="name">{{v.name}}</span>
      </router-link>
    </div>
    <div class="right companyName">
      <router-link
        v-for="v in listNavItem"
        v-bind:key="v.id"
        :to="{path:'/detail',query:{id:v.id}}"
      >
        <p>{{v.title}}</p>
      </router-link>
    </div>
  </div>
</template>
<script>
export default {
  name: "Index",
  data() {
    return {
      listNav: [],
      listNavItem: [],
      isActive: 0
    };
  },
  beforeMount() {
    this.http.get('amouse.index.getFlList').then(res=>{
      this.listNav=res.data.list
    })
    this.http.get('amouse.index.amouseContacts',{pcateid:23}).then(res=>{
      this.listNavItem=res.data.list
    })
  },
  methods: {
    switchMenu(...e) {
      this.isActive = e[0];
      this.http.get("amouse.index.amouseContacts",{pcateid:e[1] }).then(res=>{
        this.listNavItem=res.data.list
      })

    }
  }
};
</script>
<style scoped>
a {
  text-decoration: none;
  color: #333;
  color: inherit;
}
.Index {
  height: 100%;
}
.isActive {
  background: white;
  color: #333;
}
.isActive span {
  color: inherit !important;
}
.Index:after {
  content: "";
  display: block;
  clear: both;
}
.classify {
  width: 30%;
  overflow: auto;
  background: #f9f9f9;
  float: left;
  border-right: 1px solid #ebebeb;
  box-sizing: border-box;
}
.classify a {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 14px;
  color: #333;
  margin-bottom: 10px;
  padding: 10px 0;
}
.classify a .name {
  margin-left: 3px;
  color: #737373;
}
.companyName {
  width: 70%;
  height: 100%;
  float: right;
  top: 0;
  right: 0;
  padding: 10px;
  color: #333;
  box-sizing: border-box;
  overflow: auto;
}
.companyName p {
  padding: 10px 0;
  line-height: 25px;
}
</style>
