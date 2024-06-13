<template>
  <div class="about">
    <div class="aboutUser">
      <div class="tabUser">
        <div v-for="(item,index) in tablist" :key="index" :class="index===idx?'active':'tabTop'"
             @click="tabChange(index)">
          <div class="tabTopSize family">{{ item.name }}</div>
        </div>
      </div>
      <div class="tabContent">
        <!-- 切换币种-->
        <div class="topContent">
          <div class="topName">
            <div v-for="(item,index) in toplist" :key="item.id"
                 :class="index===indexNum?'topActive family':'topNameSize family'"
                 @click="topChange(index)">
              <el-image :src="item.url" style="width: 30px;height: 30px"></el-image>
              <div class="topSize">{{ item.name }}</div>
            </div>
          </div>
          <div class="topRight">BounceBit Native LSD 🌟</div>
        </div>
        <!--详细内容-->
        <div class="topMyInfo">
          <div class="MyInfo">
            <div>
              <div class="infoName family">Total Stake</div>
              <div class="infoNum family">0 BBTC</div>
            </div>
            <div>
              <div class="infoName family">APR</div>
              <div class="infoNum family">4 %</div>
            </div>
            <div>
              <div class="infoName family">My Stake</div>
              <div class="infoNum family">0 stBBTC</div>
            </div>
          </div>
          <el-divider border-style="dashed" v-if="indexNum===1"/>
          <div class="Rewards" v-if="indexNum===1">
            <div>
              <div class="RewardsName family">My Rewards</div>
              <div class="RewardsSize">0 BB</div>
            </div>
            <div class="RewardsButton family">Claim Rewards</div>
          </div>
        </div>

        <!--切换类型数据-->
        <div class="tabDate" v-if="idx===1">
          <div class="tabDateLeft">
            <div v-for="(item,index) in tabDate" :key="index"
                 :class="idxDate===index?'tabDateActive family':'tabDateLeftName family'" @click="requestChange(index)">
              {{ item.name }}
            </div>
          </div>
          <div class="tabDateRight">Pending amount: <span style="color: #000">BB</span></div>
        </div>

        <div class="ReadyClaim" v-if="idxDate===1">
          <div class="ReadyClaimLeft"></div>
          <div class="ReadyClaimRight family">Ready to Claim</div>
        </div>

        <!-- 我的余额信息-->
        <div class="balance" v-if="idxDate===0">
          <div class="balanceNum">
            <div class="balanceLeft">0.00</div>
            <div class="balanceRight">
              <el-image src="/image/icon10.png" style="width:40px;height: 40px;margin: 0 10px"></el-image>
              BBTC
            </div>
          </div>
          <div class="balanceTitle">Balance: 0 Max</div>
        </div>
        <!--提示信息-->
        <div class="title family" v-if=" idxDate===0">
          <el-icon size="20px" color="#978365">
            <Warning/>
          </el-icon>
          <div class="titleSize">Requested token will be available to claim after 1 day.</div>
        </div>
        <div class="title family" style="background-color: #EBEBE9" v-if="idxDate===0">
          <el-icon size="20px" color="#7E7E77">
            <Warning/>
          </el-icon>
          <div class="titleSize">Requested token will be available to claim after 1 day.</div>
        </div>

        <!-- 连接钱包-->
        <div class="bottomBtn family" @click="connectChange"> Connect Wallet</div>
        <!--汇率换算-->
        <div class="compute family" v-if="idxDate===0">
          <div>You Will Receive</div>
          <div>0 stBBTC</div>
        </div>
        <div class="compute family" v-if="idxDate===0">
          <div>Exchange Rate</div>
          <div>1 BBTC = 1 stBBTC</div>
        </div>
      </div>
    </div>
  </div>
  <!-- 登录弹窗信息 -->
  <DialogLogin ref="Login"></DialogLogin>
</template>

<script setup>
import {ref} from 'vue'
import DialogLogin from "@/components/DialogLogin/DialogLogin.vue";
import {Warning} from '@element-plus/icons-vue'

const tablist = ref([
  {
    name: "STAKE"
  }, {
    name: "UNSTAKE"
  },
])
const toplist = ref([
  {
    name: 'BB',
    url: 'https://portal.bouncebit.io/assets/coin/bouncebit.svg',
  }, {
    name: 'BBTC',
    url: '/image/icon10.png',
  },
])
const tabDate = ref([
  {
    name: 'Request'
  }, {
    name: 'Claim'
  },
])
let idx = ref(0)
let indexNum = ref(0)
let idxDate = ref(0)
const Login = ref(null)


function connectChange() {
  Login.value.openChange()
}

function tabChange(val) {
  idx.value = val
}

function topChange(val) {
  indexNum.value = val
}

function requestChange(val) {
  idxDate.value = val

}
</script>

<style lang="scss" scoped>
::v-deep(.el-divider--horizontal) {
  margin: 10px 0;
}

.about {
  width: 100%;
  height: calc(100vh - 100px);
  background-image: url("~@/assets/icon1.png");
  background-size: 100% 100%;
  background-repeat: no-repeat;
  display: flex;
  justify-content: center;
  align-items: center;
  padding-bottom: 100px;

  .aboutUser {
    width: 800px;
    height: 600px;

    .tabContent {
      width: 800px;
      background-color: #ffffff;
      border-radius: 0 10px 10px 10px;
      border: 1px solid #978365;
      margin-top: -1px;
      padding: 0 20px;
      padding-bottom: 20px;

      .compute {
        display: flex;
        justify-content: space-between;
        margin-top: 10px;
        color: #92928C;
      }

      .bottomBtn {
        width: 100%;
        height: 60px;
        background-color: #978365;
        color: #EEEADD;
        border-radius: 10px;
        box-shadow: 0px -4px 0px 0px rgba(59, 53, 43, .5) inset;
        margin-top: 20px;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 20px;
        cursor: pointer;
      }

      .title {
        width: 100%;
        height: 40px;
        line-height: 40px;
        background-color: #EEEADD;
        box-sizing: border-box;
        padding: 0 20px;
        margin-top: 20px;
        display: flex;
        align-items: center;
        border-radius: 10px;

        .titleSize {
          margin-left: 20px;
          color: #978365;
        }
      }

      .tabDate {
        display: flex;
        border-bottom: 1px solid #978365;
        margin-top: 30px;
        align-items: center;
        justify-content: space-between;

        .tabDateRight {
          color: #92928C;
          font-size: 20px;
          font-weight: 600;
        }

        .tabDateLeft {
          display: flex;

          .tabDateActive {
            cursor: pointer;
            font-size: 20px;
            width: 150px;
            height: 50px;
            background-color: #EEEADD;
            border-top-left-radius: 10px;
            border-top-right-radius: 10px;
            text-align: center;
            line-height: 50px;
            color: #978365;
          }

          .tabDateLeftName {
            cursor: pointer;
            font-size: 20px;
            width: 150px;
            height: 50px;
            border-top-left-radius: 10px;
            border-top-right-radius: 10px;
            text-align: center;
            line-height: 50px;
            color: #978365;
          }
        }
      }

      .ReadyClaim {
        width: 100%;
        height: 100px;
        border: 1px solid #978365;
        border-radius: 10px;
        margin-top: 30px;
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 0 20px;
        box-sizing: border-box;
        .ReadyClaimLeft{
          width: 80%;
          height: 100px;
        }
        .ReadyClaimRight{
          width: 150px;
          height: 50px;
          text-align: center;
          line-height: 50px;
          border: 1px solid #519C7A;
          color: #519C7A;
          background-color: #E9F9EE;
          margin-left: 10px;
          border-radius: 10px;
          font-size: 16px;
          cursor: pointer;
        }
      }

      .balance {
        width: 100%;
        background-color: #FBF9F2;
        border: 1px solid #978365;
        border-radius: 8px;
        box-sizing: border-box;
        padding: 10px;
        margin-top: 20px;

        .balanceTitle {
          text-align: right;
          font-family: Fugaz One, sans-serif;
          font-weight: 600;
          color: #979591;
        }

        .balanceNum {
          display: flex;
          justify-content: space-between;
          align-items: center;
          margin-top: 30px;

          .balanceLeft {
            font-family: Fugaz One, sans-serif;
            font-weight: 600;
            font-size: 60px;
            font-style: italic;
            color: #979591;
          }

          .balanceRight {
            font-size: 26px;
            font-weight: 600;
            font-family: Fugaz One, sans-serif;
            display: flex;
            align-items: center;
          }
        }
      }

      .topMyInfo {
        width: 100%;
        background-color: #ffffff;
        border: 1px solid #978365;
        border-radius: 8px;
        box-sizing: border-box;
        padding: 0 20px;

        .Rewards {
          display: flex;
          justify-content: space-between;
          margin: 20px 0;

          .RewardsButton {
            height: 60px;
            width: 200px;
            background-color: #978365;
            border-radius: 10px;
            text-align: center;
            line-height: 60px;
            color: #ffffff;
            font-size: 20px;
            font-weight: 600;
            cursor: pointer;
          }

          div {
            .RewardsName {
              color: #92928C;
              font-size: 20px;
              font-weight: 600;
            }

            .RewardsSize {
              font-size: 20px;
              font-weight: 600;
              color: #978365;
            }
          }
        }

        .MyInfo {
          height: 100px;
          display: flex;
          justify-content: space-between;

          div {
            margin-top: 10px;

            .infoName {
              color: #92928C;
              font-size: 20px;
              font-weight: 600;
            }

            .infoNum {
              font-size: 20px;
              font-weight: 600;
              color: #978365;
            }
          }
        }
      }

      .topContent {
        height: 80px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-top: 10px;


        .topName {
          display: flex;
          align-items: center;
          justify-content: space-between;

          .topActive {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px;
            width: 100px;
            background-color: #EEEADD;
            border-radius: 8px;
            cursor: pointer;

            .topSize {
              margin-right: 20px
            }
          }

          .topNameSize {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px;
            width: 100px;
            background-color: #ffffff;
            border-radius: 8px;
            cursor: pointer;

            .topSize {
              margin-right: 20px
            }
          }
        }

        .topRight {
          color: #3B8D69;
          font-size: 20px;
          font-weight: 600;
        }
      }
    }

    .tabUser {
      display: flex;

      .active {
        width: 150px;
        height: 60px;
        text-align: center;
        line-height: 60px;
        border-top: 1px solid #978365;
        border-left: 1px solid #978365;
        border-right: 1px solid #978365;
        border-radius: 10px 10px 0 0;
        background-color: #ffffff;

        .tabTopSize {
          font-weight: bold;
          font-size: 28px;
          color: #000;
          font-style: italic;
          cursor: pointer;
        }
      }

      .tabTop {
        width: 150px;
        height: 60px;
        text-align: center;
        line-height: 60px;
        border-top: 1px solid #978365;
        border-left: 1px solid #978365;
        border-right: 1px solid #978365;
        border-radius: 10px 10px 0 0;
        background-color: #EEEADD;

        .tabTopSize {
          width: 151px;
          font-weight: bold;
          font-size: 28px;
          color: #978365;
          font-style: italic;
          cursor: pointer;
          margin: -1px;
          border-bottom: 1px solid #978365;
        }
      }
    }
  }
}
</style>