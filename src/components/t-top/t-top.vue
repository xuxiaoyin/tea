<template>
  <div class="top-wrap">
    <div class="top">
      <div class="pagesize">
        <a href="#" class="top-item">帮助中心</a>
        <a href="#" class="top-item">我的订单</a>
        <a href="#" class="top-item icon-register icon">注册</a>
        <a href="#" class="top-item icon-login icon">登录</a>
      </div>
    </div>

    <div class="middle pagesize">
      <div class="logo">
        <a href="/"><img src="./logo.png"> </a>
      </div>

      <div class="section-right">
        <div class="search">
          <div class="search-wrap" id="search">
            <div class="select">
              <el-select v-model="value" placeholder="请选择">
                <el-option
                  v-for="item in options"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value">
                </el-option>
              </el-select>
            </div>

            <div class="input">
              <el-autocomplete
                popper-class="my-autocomplete"
                v-model="state3"
                :fetch-suggestions="querySearch"
                placeholder="请输入内容"
                @select="handleSelect">
                <template slot-scope="{ item }">
                  <div class="name">{{ item.value }}</div>
                  <span class="addr">{{ item.address }}</span>
                </template>
              </el-autocomplete>
            </div>

            <div class="search-btn">
              <a href="javascript:">搜索</a>
            </div>
            
          </div>
          <div class="search-tip">
            <span class="name">您可能要搜：</span>
            <a href="javascript:" class="tip-item">新茶</a>
            <a href="javascript:" class="tip-item">新茶</a>
            <a href="javascript:" class="tip-item">新茶</a>
            <a href="javascript:" class="tip-item">新茶</a>
          </div>
        </div>

        <div class="phnoe">
          客服电话：020-88886548
        </div>

        <div class="cart">
          <a href="javascript:">购物车：<span>0</span>件</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      options: [
        {
          value: '选项1',
          label: '行情参考'
        },
        {
          value: '选项2',
          label: '品牌批发'
        }
      ],
      value: '',
      restaurants: [],
      state3: ''
    }
  },
      methods: {
      querySearch(queryString, cb) {
        var restaurants = this.restaurants;
        var results = queryString ? restaurants.filter(this.createFilter(queryString)) : restaurants;
        // 调用 callback 返回建议列表的数据
        cb(results);
      },
      createFilter(queryString) {
        return (restaurant) => {
          return (restaurant.value.toLowerCase().indexOf(queryString.toLowerCase()) === 0);
        };
      },
      loadAll() {
        return [
          { "value": "三全鲜食（北新泾店）", "address": "长宁区新渔路144号" },
          { "value": "Hot honey 首尔炸鸡（仙霞路）", "address": "上海市长宁区淞虹路661号" },
          { "value": "新旺角茶餐厅", "address": "上海市普陀区真北路988号创邑金沙谷6号楼113" },
          { "value": "泷千家(天山西路店)", "address": "天山西路438号" },
          { "value": "南拳妈妈龙虾盖浇饭", "address": "普陀区金沙江路1699号鑫乐惠美食广场A13" }
        ];
      },
      handleSelect(item) {
        console.log(item);
      }
    },
    mounted() {
      this.restaurants = this.loadAll();
    }
}
</script>

<style lang="stylus" scoped>
@import '~common/stylus/variable';
.top-wrap
  .top
    height: 30px;
    background: #f1f1f1;
    text-align: right;
    font-size 0;
    .top-item
      display: inline-block;
      margin-left: 34px;
      height:18px;
      line-height: 18px;
      margin-top: 6px;
      font-size: 12px;
    .icon
      padding-left: 22px;
      background: url(./top-icon.png) no-repeat 0 0;
    .icon-register
      background-position: 0 -18px;
    .top-item:hover
      color: $color-text-r;
  .middle
    display: flex;
    height: 90px;
    align-items: center;
    .logo
      flex: 0 0 302px;
      width: 302px;
    .section-right
      flex: 1;
      display: flex;
      justify-content: space-between;
      .search
        flex: 0 0 480px;
        width: 480px;
        #search
          display: flex;
          height: 38px;
          border: 1px solid #d3d3d3;
          .select
            flex: 0 0 105px;
            width: 105px;
            height: 32px;
            margin-top: 3px;
          .select>>> .el-input__inner
            height: 32px;
            border: none;
            border-right: 1px solid #d3d3d3;
            border-radius: 0;
          .select>>>  .el-input__suffix
            top: 3px;
          .input
            flex: 0 0 280px;
            width: 280px;
          .input>>> .el-input__inner
            width: 280px;
            height: 38px;
            border: none;
          .search-btn
            flex: 1;
            a 
              height: 40px;
              display: block;
              line-height: 40px;
              margin-top: -1px;
              padding-left: 30px;
              background: $color-background-theme url(./search.png) no-repeat 14px center;
              color: #fff;
              text-align: center;
              font-size: 16px;
        .search-tip
          line-height: 28px;
          font-size: 12px;
          .name
            color: #b3b3b3;
            margin-right: 10px;
          .tip-item
            margin-right: 20px;
            color: $color-text-r;
      .phnoe
        flex: 1;
        line-height: 40px;
        text-align: center;
      .cart
        flex: 0 0 170px;
        width: 170px;
        height: 40px;
        line-height: 40px;
        text-align: center;
        box-sizing: border-box;
        border: 1px solid #d9d9d9;
        a
          display: block;
          padding-left: 22px;
          background: url(./cart.png) no-repeat 32px center;
          span 
            color: $color-text-r;
            margin: 0 4px;
</style>

