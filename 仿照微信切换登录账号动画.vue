<template>
  <div class="loginWrap">
    <div
      class="item"
      :class="{disable:isLoading && item !== loadUser}"
      v-for="(item,index) in userList"
      :key="index"
      @click="handleChange(item)"
    >
      <div class="left">
        <img
          src="https://dss1.baidu.com/70cFfyinKgQFm2e88IuM_a/forum/pic/item/a8773912b31bb051ca274cbc387adab44aede027.jpg"
        />
      </div>
      <div class="right">
        <div class="topWrap" :class="distDirect(item)?'lineHei60px':'lineHei37px'">No.{{index}}</div>
        <div class="botWrap">
          <div class="bot" v-show="item === curUser">当前使用</div>
          <div class="bot2" v-show="item === loadUser">正在登陆.</div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "videoPage",
  data() {
    return {
      loadUser: "",
      curUser: "one",
      isLoading: false,
      userList: ["one", "two", "three", "four", "five"]
    };
  },
  computed: {
    showLoading() {
      return false;
    }
  },
  mounted() {},
  methods: {
    distDirect(item) {
      //true lineHei60px'  false 'lineHei37px
      if (item === this.loadUser || item === this.curUser) {
        //有字 登录中/当前使用
        return false;
      }
      return true;
    },
    handleChange(item) {
      this.isLoading = true;
      this.loadUser = item;
      this.curUser = "";
      this.$nextTick(() => {
        setTimeout(() => {
          this.isLoading = false;
          this.loadUser = "";
          this.curUser = item;
        }, 1000);
      });
    }
  }
};
</script>
<style  scoped lang='less'>
.loginWrap {
  height: 100vh;
  color: #333333;
  font-size: 14px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  .item {
    display: flex;
    height: 60px;
    overflow: hidden;
    padding: 0 7px;
    border: 1px solid #eeeeee;
    border-radius: 4px;
    margin: 5px 0;
    .left {
      margin-right: 5px;
      width: 50px;
      display: flex;
      justify-content: center;
      align-items: center;
      img {
        width: 44px;
        height: 44px;
        border-radius: 4px;
      }
    }
    .right {
      flex: 1;
    }
    .topWrap {
      height: 33px;
      transition: all 0.5s;
      &.lineHei60px {
        line-height: 60px;
      }
      &.lineHei37px {
        line-height: 37px;
      }
    }
    .botWrap {
      height: 20px;
    }
    &.disable {
      background: #f5f5f5;
      color: #dcd7d7;
    }
    div {
      &.bot2 {
        font-size: 12px;
        color: #666;
        background: #ffffff;
        border-radius: 2px;
        width: 54px;
        text-align: center;
        margin: 0;
      }
      &.bot {
        font-size: 12px;
        color: #18e24e;
        background: #f5f5f5;
        border-radius: 2px;
        width: 54px;
        text-align: center;
        margin: 0;
      }
    }
  }
}
</style>
