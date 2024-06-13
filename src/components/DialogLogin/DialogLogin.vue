<template>
  <!-- 背景 -->
  <div class="login" v-if="dilaog">
    <!-- 内容信息 -->
    <div class="loginInfo">
      <div class="close" @click="closeChange">
        <el-image style="width: 40px; height: 40px;background-color: #EEEADD;border-radius: 50%;padding: 10px"
                  src="/image/icon3.png"/>
      </div>
      <div class="loginIcon">
        <el-image style="width: 200px; height: 200px;margin: 0 auto" src="/image/icon2.png"/>
      </div>
      <div class="loginSize">
        CONNECT WALLET
      </div>
      <div class="loginRole">
        <div v-for="(item,index) in RoleList" :key="index" class="roleInfo">
          <el-image
              style="width: 30px; height: 30px;background-color: #EEEADD;border-radius: 50%;padding: 10px;margin-left: 30px"
              :src="item.url"/>
          <div class="RoleSize">{{ item.name }}</div>
        </div>
        <div class="loginLine">
          <div class="lineLeft">
            <el-divider style="color:red" />
            <el-divider />
            <el-divider />
          </div>
          <div class="lineSize">BOUNCEBIT</div>
          <div class="loginRight">
            <el-divider />
            <el-divider />
            <el-divider />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import {ref,defineExpose} from "vue";

const RoleList = ref( [
      {
        name: 'MetaMask',
        url: '/image/icon4.png'
      }, {
      name: 'WalletConnect',
      url: '/image/icon5.png'
    }, {
      name: 'Binance Web3 Wallet',
      url: '/image/icon7.png'
    }, {
      name: 'OKX Wallet',
      url: '/image/icon6.png'
    }, {
      name: 'Bitget Wallet',
      url: '/image/icon8.png'
    }, {
      name: 'Trust Wallet',
      url: '/image/icon9.png'
    },
    ])
const dilaog=ref(false)

function closeChange(){
  dilaog.value=false
}

function openChange(){
  dilaog.value=true
}

defineExpose({ // 导出 函数 ，父组件可以使用
  openChange
})
</script>

<style lang="scss" scoped>
::v-deep(.el-divider--horizontal){
  margin: 16px 0;
}
.login {
  position: absolute;
  top: 0;
  width: 100%;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.3);
  display: flex;
  justify-content: center;
  padding-bottom: 100px;

  .loginInfo {
    height: 100vh;
    width: 600px;
    background-color: #FBF9F2;
    padding: 0 20px;
    overflow: hidden;

    .loginRole {
      width: 100%;
      background-color: #fff;
      border-radius: 20px;
      border: 1px solid #978365;
      margin-top: 20px;
      padding: 10px;
      box-sizing: border-box;
      .loginLine{
        display: flex;
        height: 40px;
        align-items: center;
        justify-content: space-between;
        margin: 20px 0;
        .lineLeft{
          width: 36%;
        }
        .loginRight{
          width: 36%;
        }
        .lineSize{
          font-size: 30px;
          font-weight: bold;
          margin: 0 10px;
        }
      }

      .RoleSize {
        font-size: 20px;
        font-weight: 600;
        color: #978365;
        margin-left: 20px;
      }

      .roleInfo {
        width: 100%;
        height: 60px;
        background-color: #FBF9F2;
        border: 1px solid #978365;
        border-radius: 10px;
        margin-top: 10px;
        display: flex;
        align-items: center;
      }

      .roleInfo:hover {
        background-color: #EEEADD;
        cursor: pointer;
      }
    }

    .loginSize {
      font-weight: 900;
      font-size: 32px;
      text-align: center;
      margin-top: 20px;
      font-style: oblique;
      font-family: Fugaz One, sans-serif;
    }

    .loginIcon {
      width: 100%;
      display: flex;
      justify-content: center;
    }

    .close {
      display: flex;
      justify-content: flex-end;
      cursor: pointer;
      padding-top: 20px;
    }
  }
}

</style>