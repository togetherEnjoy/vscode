<template>
  <div class="supplier_box">
    <smenu
      :item="item"
      :showCity="false"
      :athor="athor"
      :two="two"
      :what="2"
      oneData="国家"
      params1="countryNum"
      params2="immigrationType"
      @get_result="get_result"
    ></smenu>
    <!-- <div class="sx_result" v-if="Object.keys(result_data).length > 0">
      <h3>筛选结果</h3>
      <div class="condition">
        <div v-for="(item,i) of result_data" :key="i" class="sel" v-if="item.html != ''">
          <p v-if="item.html != ''" :typed="item.type">
            <span>{{ item.html }}</span>
            <i>
              <span @click.self="empty"></span>
            </i>
          </p>
        </div>
      </div>
    </div> -->

    <!-- <div class="thinklike" v-if="Object.keys(result_data).length > 0" @click="emptyall">
      <span></span>
      清空所有条件
    </div> -->

    <div class="supplier">
      <!-- <h3 class="like" v-if="Object.keys(result_data).length > 0">猜您喜欢</h3> -->
      <van-list
        v-model="loading"
        :finished="finished"
        finished-text="没有更多了"
        @load="onLoad"
        :offset="10"
      >
        <div class="s_item" v-for="(item, i) in allListData" :key="i">
          <div class="heads_img" @click="$router.push({path: `/${cityJX}/merchant`,query:{id:item.id}})">
            <img v-lazy="item.headPortrait">
          </div>

          <div class="text">
            <h3>{{ item.simpleName }}</h3>
            <p>咨询量：{{ item.actualNumber }}</p>
          </div>

          <div class="func">
            <span @click="zixun(); clickRate(item.id)">
              <i class="email"></i>
            </span>
            <span class="pb" @click="clickRate(item.id)">
              <a :href="`tel:${item.xuNiPhone||phone}`" class="phone"></a>
            </span>
          </div>
        </div>
      </van-list>
    </div>
  </div>
</template>

<script>
import smenu from "./slideMenu";
import { screen_data,clickRate,setCountryMode,phone } from "../utils/mixins";
export default {
  name: 'more',
  mixins: [screen_data,clickRate,setCountryMode,phone],
  props: {
    item: {
      type: Array
    },
    athor: {
      type: Array
    },
    two: {
      type: Array
    },
    myPhone: {},

    id: {},
    url: {},
    params1: {},
    params2: {}
  },
  data() {
    return {
      canmetaInfo: false,
      merchant_data: [],
      // url: `/dhr/business/immigrant/support`
    };
  },
  methods: {
    onLoad() {
      this.getAllList(this.result_data);
    },

    zixun() {
      this.$parent.showToast();
    }
  },

  components: {
    smenu
  }
};
</script>

<style scoped lang="scss">
.supplier_box {
  background-color: #f8f8f8;
  padding-top: 100px;
  .supplier {
    margin-top: 30px;
    padding: 0 30px;
    background-color: #fff;
    .s_tit {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 10px;
      h3 {
        font-size: 34px;
        font-weight: 500;
      }
      .s_huan {
        font-size: 24px;
        p {
          color: #3db484;
          position: relative;
          padding-left: 25px;
          &::after {
            position: absolute;
            content: "";
            width: 18px;
            height: 18px;
            background: url("../assets/images/immig/refresh.png") no-repeat
              center / cover;
            left: 0;
            top: 6px;
          }
          span {
            color: #9399a5;
            margin-left: 30px;
          }
        }
      }
    }

    .s_item {
      display: flex;
      padding: 32px 0;
      align-items: center;
      border-bottom: 1px solid #e5e5e5;
      .heads_img {
        width: 100px;
        height: 100px;
        border-radius: 50%;
        overflow: hidden;
        img {
          height: 100%;
        }
      }
      .text {
        margin-left: 30px;
        margin-right: auto;
        h3 {
          font-size: 30px;
          font-weight: 500;
        }
        p {
          font-size: 24px;
          margin-top: 15px;
          font-weight: 500;
          color: #9399a5;
        }
      }
      .func {
        display: flex;

        span {
          width: 48px;
          height: 48px;
          border-radius: 50%;
          background-color: #fde9ea;
          text-align: center;
          i,
          a {
            display: inline-block;
            width: 48px;
            height: 48px;
          }
        }
        .pb {
          margin-left: 30px;
        }
        .email {
          background: url("../assets/images/immig/email.png") no-repeat center /
            30px;
        }
        .phone {
          background: url("../assets/images/immig/phone.png") no-repeat center /
            30px;
        }
      }
    }
  }
}
</style>
