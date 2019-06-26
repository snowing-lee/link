<template>
  <div class="all">
    <div class="link">
      <div class="title">{{ msg }}</div>
      <div>
        提示:
        <div class="tip">{{ tip1 }}</div>
      </div>

      <div class="link-href">
        <div  class="link-th" v-for="(item, index) of list" :key="index">
          <h2>{{item.th}}</h2>
          <ul>
            <li><a class="aaa" :href="item.homeWork">作业上传</a></li>
            <br>
            <li><a class="aaa" :href="item.homeWorkGather">作业汇总</a></li>
            <br>
            <li><a class="aaa" :href="item.seatingChart">座位表</a></li>
            <br>
            <li><a class="aaa" :href="item.information">资料</a></li>
          </ul>
        </div>
      </div>

      <br>
      <div class="foot">
        <a :href="dormitory">宿舍安排</a>
        <br>
        <br>
        <a :href="meeting">周会进度</a>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'HelloWorld',
  data() {
    return {
      tip1: '1,作业提交及作业汇总情况查看时,确认已连接局域网(网线或wangdao-meeting)',
      msg: '资料汇总',
      dormitory: '',
      meeting: '',
      list: [],
    };
  },
  methods: {
    getHomeInfo() {
      // tomcat下远程
      axios.get('/link/static/mock/index.json')
        .then(this.getHomeInfoSucc);

      // 本地调试
      // axios.get('/static/mock/index.json')
      //   .then(this.getHomeInfoSucc);
    },
    getHomeInfoSucc(res) {
      const res1 = res.data;
      if (res1.ret && res1.data) {
        const data1 = res1.data;
        this.list = data1.list;
        this.dormitory = data1.dormitory;
        this.meeting = data1.meeting;
      }
    },
  },
  mounted() {
    // 生命周期函数
    this.getHomeInfo();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.link {
  margin-left: 4rem;

}
  .title {
    margin-left: 5rem;
    font-size: 200%;
    text-align: center;
  }
  .tip {
    color: red;
    margin-left: 5rem;
    font-size: 80%;
  }
  .link-href {
    margin-top: 2rem;
    width: 100%;
    height: 20rem;
    border:1px solid
  }
    .link-th {
      margin-left: 6rem;
      float: left;
    }
  .aaa {
    line-height: 1rem;
  }
.foot {
  margin-bottom: 5rem;
}
</style>
