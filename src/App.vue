<!--
 * @Description: In User Settings Edit
 * @Author: y
 * @Date: 2019-09-16 21:27:04
 * @LastEditTime: 2019-09-17 15:03:36
 * @LastEditors: Please set LastEditors
 -->
<template>
  <div id="app">
    <tableCMM v-bind:tableArr="tableArr" :header="header" :pageSize="2"></tableCMM>
  </div>
</template>

<script>
import tableCMM from "./components/tableCMM.vue";

export default {
  name: "app",
  data() {
    return {
      tableArr: [
        {
          td1: 2,
          td2: "b",
          td3: "哦哦"
        },
        {
          td1: 1,
          td2: "a",
          td3: "啊啊"
        },
        {
          td1: 3,
          td2: "c",
          td3: "嘿嘿"
        },
        {
          td1: 5,
          td2: "c",
          td3: "嘿嘿"
        },
        {
          td1: 6,
          td2: "c",
          td3: "嘿嘿"
        },
        {
          td1: 4,
          td2: "a",
          td3: "啊啊"
        }
      ],
      header: ["序号", "字母", "内容"]
    };
  },
  components: {
    tableCMM
  },
  created: function() {
    // console.log(this.tableArr);
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
