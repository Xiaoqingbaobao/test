<template>
  <div id="app">
    <van-nav-bar
      background="rgba(237, 237, 237)"
      :class="this.listData.length > 1 ? 'addbor' : 'noborder'"
      title="微信支付"
      left-arrow
    >
      <template #left>
        <van-icon name="arrow-left" size="22" color="#333" />
      </template>
      <template #right>
        <van-icon class="search" name="search" size="22" color="#333" />
        <svg
          width="22"
          height="22"
          viewBox="0 0 48 48"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
          @click="setting()"
        >
          <path
            d="M36.686 15.171C37.9364 16.9643 38.8163 19.0352 39.2147 21.2727H44V26.7273H39.2147C38.8163 28.9648 37.9364 31.0357 36.686 32.829L40.0706 36.2137L36.2137 40.0706L32.829 36.686C31.0357 37.9364 28.9648 38.8163 26.7273 39.2147V44H21.2727V39.2147C19.0352 38.8163 16.9643 37.9364 15.171 36.686L11.7863 40.0706L7.92939 36.2137L11.314 32.829C10.0636 31.0357 9.18372 28.9648 8.78533 26.7273H4V21.2727H8.78533C9.18372 19.0352 10.0636 16.9643 11.314 15.171L7.92939 11.7863L11.7863 7.92939L15.171 11.314C16.9643 10.0636 19.0352 9.18372 21.2727 8.78533V4H26.7273V8.78533C28.9648 9.18372 31.0357 10.0636 32.829 11.314L36.2137 7.92939L40.0706 11.7863L36.686 15.171Z"
            fill="none"
            stroke="#333"
            stroke-width="3"
            stroke-linejoin="round"
          />
          <path
            d="M24 29C26.7614 29 29 26.7614 29 24C29 21.2386 26.7614 19 24 19C21.2386 19 19 21.2386 19 24C19 26.7614 21.2386 29 24 29Z"
            fill="none"
            stroke="#333"
            stroke-width="3"
            stroke-linejoin="round"
          />
        </svg>
      </template>
    </van-nav-bar>
    <ul class="contant">
      <li v-for="(item, index) in listData">
        <div class="time">{{ item.time }}</div>
        <div class="box">
          <div class="title">收款到账通知</div>
          <div class="momey">收款金额</div>
          <div class="momey_number">
            <span class="symbol">{{ item.money }}</span>
          </div>
          <div class="flex">
            <span>汇总</span>
            <div>
              今日第{{ index + 1 }}笔收款，共计￥{{ item.aggregateAmount }}
            </div>
          </div>
          <div class="flex">
            <span>备注</span>
            <div>收款成功，已存入零钱。点击可查看详情</div>
          </div>
          <div class="border_line"></div>
          <div class="details">
            <div>收款小账本</div>
            <div class="symbol_right">
              <van-icon name="arrow" />
            </div>
          </div>
        </div>
      </li>
    </ul>
    <van-popup v-model:show="showBottom" position="bottom">
      <ul class="amount">
        <li v-for="(item, index) in numberData" @click="add(item)">
          +{{ item }}
        </li>
        <li @click="clearList">清空</li>
        <li @click="unpopover">取消</li>
      </ul>
    </van-popup>
    <div class="bottom_box">
      <span
        ><svg
          t="1678488867845"
          class="icon"
          viewBox="0 0 1024 1024"
          version="1.1"
          xmlns="http://www.w3.org/2000/svg"
          p-id="8307"
          width="26"
          height="26"
        >
          <path
            d="M512 65c246.319 0 446 199.681 446 446S758.319 957 512 957 66 757.319 66 511 265.681 65 512 65z m0 59.773c-213.307 0-386.227 172.92-386.227 386.227S298.693 897.227 512 897.227 898.227 724.307 898.227 511 725.307 124.773 512 124.773z m140.227 549.454c12.702 0 23 10.297 23 23v34.464c0 12.702-10.298 23-23 23H374.072c-12.702 0-23-10.298-23-23v-34.464c0-12.703 10.298-23 23-23h278.155zM466.01 500.655c12.703 0 23 10.297 23 23v64.35c0 12.703-10.297 23-23 23h-66.65c-12.702 0-23-10.297-23-23v-64.35c0-12.703 10.298-23 23-23h66.65z m160.928 0c12.703 0 23 10.297 23 23v64.35c0 12.703-10.297 23-23 23h-66.65c-12.702 0-23-10.297-23-23v-64.35c0-12.703 10.298-23 23-23h66.65z m-324.154-1.15c12.702 0 23 10.298 23 23v64.35c0 12.703-10.298 23-23 23h-66.65c-12.703 0-23-10.297-23-23v-64.35c0-12.702 10.297-23 23-23h66.65z m487.38 0c12.703 0 23 10.298 23 23v64.35c0 12.703-10.297 23-23 23h-66.649c-12.702 0-23-10.297-23-23v-64.35c0-12.702 10.298-23 23-23h66.65zM466.01 339.727c12.703 0 23 10.297 23 23v64.35c0 12.703-10.297 23-23 23h-66.65c-12.702 0-23-10.297-23-23v-64.35c0-12.703 10.298-23 23-23h66.65z m160.928 0c12.703 0 23 10.297 23 23v64.35c0 12.703-10.297 23-23 23h-66.65c-12.702 0-23-10.297-23-23v-64.35c0-12.703 10.298-23 23-23h66.65z m-324.154-1.15c12.702 0 23 10.298 23 23v64.35c0 12.703-10.298 23-23 23h-66.65c-12.703 0-23-10.297-23-23v-64.35c0-12.702 10.297-23 23-23h66.65z m487.38 0c12.703 0 23 10.298 23 23v64.35c0 12.703-10.297 23-23 23h-66.649c-12.702 0-23-10.297-23-23v-64.35c0-12.702 10.298-23 23-23h66.65z"
            fill="#333333"
            p-id="8308"
          ></path></svg
      ></span>
      <ul class="botton_txt">
        <li>我的账单</li>
        <li>支付服务</li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      showBottom: false,
      listData: [],
      numberData: ["20", "12", "18.80", "25"],
    };
  },
  methods: {
    clearList() {
      this.listData = [];
      this.showBottom = false;
    },
    setting() {
      this.showBottom = true;
    },
    unpopover() {
      this.showBottom = false;
    },
    add(item) {
      item = Number(item);
      let aggregateAmount = 0;
      this.listData.forEach(
        (item) => (aggregateAmount = aggregateAmount + Number(item.money))
      );
      aggregateAmount = aggregateAmount + item;
      let hour = new Date().getHours();
      if (hour < 10) {
        hour = "0" + hour;
      }
      let minute = new Date().getMinutes();
      if (minute < 10) {
        minute = "0" + minute;
      }
      console.log(hour, minute);
      let time = hour + ":" + minute;
      this.listData.push({
        money: item.toFixed(2),
        time: time,
        aggregateAmount: aggregateAmount.toFixed(2),
      });
      this.showBottom = false;
    },
  },
};
</script>
<style lang="less">
html,
body,
#app {
  height: 100%;
  .amount {
    text-align: center;
    li {
      height: 60px;
      line-height: 60px;
      border-bottom: 1px solid #ccc;
    }
  }
  // font-family:"Microsoft Yahei";
  .search {
    margin-right: 20px;
  }
  background: rgba(237, 237, 237);
  .van-nav-bar {
    background: rgba(237, 237, 237);
    position: fixed;
    width: 100%;
    top: 0;
    padding-top: 28px;
  }
  .addbor {
    border-bottom: 0.5px solid #ccc;
  }
  .noborder {
    border-bottom: 1px solid transparent;
  }
  .contant {
    margin: 0% 5%;
    padding: 30px 0 80px 0;

    li {
      .time {
        color: rgb(169, 169, 169);
        text-align: center;
        font-size: 14px;
        margin: 12px 0 15px 0;
        padding-top: 10px;
      }
      .box {
        border-radius: 5px;
        padding: 0 6%;

        background: #fff;
        .title {
          font-size: 16px;
          padding: 24px 0;
        }
        .momey {
          text-align: center;
          font-size: 14px;
          color: rgb(140, 140, 140);
        }
        .momey_number {
          font-family: "微软雅黑";
          text-align: center;
          font-weight: 500;
          span {
            font-size: 38px;
            position: relative;
            &::after {
              font-family: "微软雅黑";
              content: "￥";
              position: absolute;
              top: 0px;
              font-size: 28px;
              left: -28px;
              font-weight: 500;
            }
          }
          margin: 10px 0 18px 0;
        }
        .flex {
          font-size: 15px;
          display: flex;
          margin-bottom: 16px;
          span {
            color: rgba(125, 125, 125);
            margin-right: 20px;
            white-space: nowrap;
          }
        }
        .border_line {
          border-bottom: 1px solid rgb(237, 237, 237);
        }
        .details {
          position: relative;
          width: 100%;
          padding: 10px 0 14px 5px;
          display: flex;
          font-size: 14px;
          justify-content: flex-between;
          .symbol_right {
            position: absolute;
            right: 0;
            padding-right: 10px;
            color: rgba(177, 177, 177);
          }
        }
      }
    }
  }
  .number_list {
    position: absolute;
  }
  .bottom_box {
    position: fixed;
    display: flex;
    align-items: center;
    bottom: 0;
    width: 100%;
    height: 60px;
    background: #f6f6f6;
    border-top: 0.5px solid #ccc;
    border-bottom: 1px solid transparent;

    span {
      margin: 0 10px;
    }
    .botton_txt {
      display: flex;
      width: 100%;
      height: 30px;
      line-height: 30px;
      text-align: center;
      font-size: 15px;
      li {
        flex: 1;
        border-left: 0.5px solid #ccc;
      }
    }
  }
}
</style>
