<template>
  <div class="header">
    <div class="headerLeft">Beenav</div>
    <div class="headerCenter">
      <div v-for="(item,idx) in menuList" :key="idx" @click="tabChange(idx,item)" :class="idx===index?'active':''">
        <el-image v-if="idx===index" style="width: 30px; height: 30px;" src="/image/icon.png" :fit="fit"/>
        <div class="headerSize"> {{ item.name }}</div>
      </div>
    </div>
    <div class="headerRight" @click="dialogChange">Connect Wallet</div>
  </div>
  <!-- 登录弹窗信息 -->
  <DialogLogin ref="Login"></DialogLogin>
  <!-- 路由导航-->
  <router-view></router-view>
</template>

<script setup>
import {ref} from 'vue'
import {useRouter} from "vue-router";
import DialogLogin from "@/components/DialogLogin/DialogLogin.vue";

const router = useRouter()
const Login = ref(null)

const menuList = ref([
  {
    name: '',
    id: 0,
  }, {
    name: '',
    id: 1,
  }, {
    name: 'Stake',
    url: '/about',
    id: 2,
  }, {
    name: '',
    id: 3,
  }, {
    name: '',
    id: 4,
  }, {
    name: '',
    id: 5,
  },
])


let index = ref(2)

function tabChange(idx, item) {
  index.value = idx
  router.push(item.url)
}

function dialogChange() {
  Login.value.openChange()
}

</script>
<style lang="scss" scoped>
.header {
  height: 100px;
  background-color: #EEEADD;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 30px;

  .headerLeft {
    font-size: 30px;
    font-weight: 800;
  }

  .headerRight {
    cursor: pointer;
    width: 190px;
    height: 3rem;
    text-align: center;
    line-height: 3rem;
    border-radius: 10px;
    font-weight: 600;
    font-size: 20px;
    background-color: #978365;
    color: #EEEADD;
    box-shadow: 0px -4px 0px 0px rgba(59, 53, 43, .5) inset;
  }

  .headerCenter {
    display: flex;
    align-items: center;
    justify-content: space-between;

    div {
      line-height: 100px;
      cursor: pointer;
    }

    .headerSize {
      font-size: 26px;
      font-weight: 600;
      margin-left: 20px;
    }

    .active {
      width: 100%;
      height: 100px;
      display: flex;
      align-items: center;
      background-color: #FBF9F2;
      padding: 0 34px;
    }
  }
}
</style>
