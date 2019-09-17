<!--
 * @Description: In User Settings Edit
 * @Author: y
 * @Date: 2019-09-16 21:27:04
 * @LastEditTime: 2019-09-17 15:08:22
 * @LastEditors: Please set LastEditors
 -->
<template>
  <div class="tableWrp">
    <button class="btn" @click="sorter">表格排序</button>
    <input class="ipt" type="text" v-model="fliterVal" v-on:input="fliterFun()" />
    <div class="table">
      <div class="tableHeader">
        <div class="td" v-for="headItem in header" :key="headItem">{{headItem}}</div>
      </div>
      <div
        class="tr"
        v-for="item in [...this.tableData.slice(this.pageCur * this.pageSizeData, this.pageSizeData * (this.pageCur + 1))]"
        :key="item.td1"
      >
        <div class="td">{{item.td1}}</div>
        <div class="td">{{item.td2}}</div>
        <div class="td">{{item.td3}}</div>
      </div>
    </div>
    <div class="pageBtnWrp">
      <span class="pageBtn" @click="pageBtnFun(pageCur)">
        <i class="wrp">
          <svg
            viewBox="64 64 896 896"
            data-icon="left"
            width="1em"
            height="1em"
            fill="currentColor"
            aria-hidden="true"
            focusable="false"
            class
          >
            <path
              d="M724 218.3V141c0-6.7-7.7-10.4-12.9-6.3L260.3 486.8a31.86 31.86 0 0 0 0 50.3l450.8 352.1c5.3 4.1 12.9.4 12.9-6.3v-77.3c0-4.9-2.3-9.6-6.1-12.6l-360-281 360-281.1c3.8-3 6.1-7.7 6.1-12.6z"
            />
          </svg>
        </i>
      </span>
      <span
        @click="pageBtnFun(item)"
        v-for="item in (Math.ceil((tableData.length) / pageSizeData))"
        :tabindex="item"
        :key="item"
        v-bind:class="{pageBtn:true,pageBtnCur: item == pageCur+1}"
      >{{item}}</span>
      <span class="pageBtn" @click="pageBtnFun(pageCur+2)">
        <i class="wrp">
          <svg
            viewBox="64 64 896 896"
            data-icon="right"
            width="1em"
            height="1em"
            fill="currentColor"
            aria-hidden="true"
            focusable="false"
            class
          >
            <path
              d="M765.7 486.8L314.9 134.7A7.97 7.97 0 0 0 302 141v77.3c0 4.9 2.3 9.6 6.1 12.6l360 281.1-360 281.1c-3.9 3-6.1 7.7-6.1 12.6V883c0 6.7 7.7 10.4 12.9 6.3l450.8-352.1a31.96 31.96 0 0 0 0-50.4z"
            />
          </svg>
        </i>
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: "tableCMM",
  data() {
    return {
      tableData: [...this.tableArr],
      pageSizeData: this.pageSize,
      pageCur: 0,
      fliterVal: ""
    };
  },
  props: {
    tableArr: Array,
    header: Array,
    pageSize: {
      type: Number,
      default: 0
    }
  },
  methods: {
    // 过滤搜索
    fliterFun: function() {
      if (this.fliterVal == "") {
        this.tableData = [...this.tableArr];
      } else {
        this.tableData = [
          ...this.tableArr.filter(item => {
            return Object.values(item).filter(item2 => {
              return item2.toString().indexOf(this.fliterVal) === 0;
            }).length;
          })
        ];
      }
    },
    // 根据td1序号进行排序
    sorter: function() {
      this.tableData.sort(function(a, b) {
        return Number(a.td1) - Number(b.td1);
      });
    },
    // 点击分页按钮
    pageBtnFun: function(e) {
      // console.log(e);
      if (e > 0 && e <= Math.ceil(this.tableData.length / this.pageSizeData)) {
        this.pageCur = e - 1;
      }
    }
  },
  created: function() {}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.table {
  width: 50%;
  display: table;
  margin: 50px auto;
}
.tr {
  display: table-row;
  transition: all 0.3s;
}
.tr:hover {
  background: rgba(24, 143, 255, 0.349);
}
.tableHeader {
  display: table-row;
  background: #fafafa;
}
.td {
  display: table-cell;
  border-top: 1px solid #e8e8e8;
  color: rgba(0, 0, 0, 0.65);
  padding: 16px;
}
.tr:last-child .td {
  border-bottom: 1px solid #e8e8e8;
}
.pageBtn {
  cursor: pointer;
  border-radius: 4px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  min-width: 32px;
  height: 32px;
  line-height: 30px;
  text-align: center;
  list-style: none;
  display: inline-block;
  vertical-align: middle;
  border: 1px solid #d9d9d9;
  background-color: #fff;
  margin-right: 8px;
  font-family: Arial;
  outline: 0;
}
.pageBtn .wrp {
  width: 100%;
  height: 100%;
  display: flex;
  text-align: center;
  justify-content: center;
  align-items: center;
}
.pageBtnCur {
  border-color: #1890ff;
  color: #1890ff;
  font-weight: 500;
}
.btn {
  line-height: 1.499;
  display: inline-block;
  font-weight: 400;
  text-align: center;
  touch-action: manipulation;
  cursor: pointer;
  background-image: none;
  border: 1px solid transparent;
  white-space: nowrap;
  padding: 0 15px;
  font-size: 14px;
  border-radius: 4px;
  height: 32px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  transition: all 0.3s cubic-bezier(0.645, 0.045, 0.355, 1);
  position: relative;
  color: #fff;
  background-color: #1890ff;
  border-color: #1890ff;
  text-shadow: 0 -1px 0 rgba(0, 0, 0, 0.12);
  box-shadow: 0 2px 0 rgba(0, 0, 0, 0.045);
  margin-bottom: 30px;
}
.ipt {
  font-variant: tabular-nums;
  box-sizing: border-box;
  margin: 0 auto;
  padding: 0;
  list-style: none;
  position: relative;
  display: block;
  padding: 4px 11px;
  width: 50%;
  height: 32px;
  font-size: 14px;
  line-height: 1.5;
  color: rgba(0, 0, 0, 0.65);
  background-color: #fff;
  background-image: none;
  border: 1px solid #d9d9d9;
  border-radius: 4px;
  transition: all 0.3s;
}
</style>
