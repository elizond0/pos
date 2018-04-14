<template>
  <div class="pos">
    <el-row>
      <el-col :span='7' class="pos-order" id='order-list'>
        <el-tabs class='order-tabs'>
          <el-tab-pane label='点餐'>
            <el-table :data='tableData' border style='width:100%'>
              <el-table-column prop='goodsName' label='商品名称'>商品名称</el-table-column>
              <el-table-column prop='count' label='数量' width='50'>数量</el-table-column>
              <el-table-column prop='price' label='金额' width='70'>金额</el-table-column>
              <el-table-column label='操作' width='100' fixed='right'>
                <template scope='scope'>
                  <el-button type='text' size='small'>删除</el-button>
                  <el-button type='text' size='small'>增加</el-button>
                </template>
              </el-table-column>
            </el-table>
            <div class='order-btn'>
              <el-button type='warning'>挂单</el-button>
              <el-button type='danger'>删除</el-button>
              <el-button type='success'>结账</el-button>
            </div>
          </el-tab-pane>
          <el-tab-pane label='挂单'>挂单</el-tab-pane>
          <el-tab-pane label='外卖'>外卖</el-tab-pane>
        </el-tabs>
      </el-col>

      <el-col :span='17'>
        <div class='often-goods'>
          <div class='title'>常用商品</div>
          <div class='often-goods-list'>
            <ul>
              <li v-for='goods in oftenGoods'>
                <span>{{goods.goodsName}}</span>
                <span class='o-price'>${{goods.price}}元</span>
              </li>
            </ul>
          </div>
        </div>
        
        <div class="goods-type">
          <el-tabs>
            <el-tab-pane label='汉堡'>
                <div>
                  <ul class="cookList">
                    <li v-for="goods in type0Goods">
                      <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                      <span class="foodName">{{goods.goodsName}}</span>
                      <span class="foodPrice">￥{{goods.price}}元</span>
                    </li>
                  </ul>
                </div>
            </el-tab-pane>
            <el-tab-pane label='小食'>
                小食
            </el-tab-pane>
            <el-tab-pane label='饮料'>
                饮料
            </el-tab-pane>
            <el-tab-pane label='套餐'>
                套餐
            </el-tab-pane>
          </el-tabs>
        </div>

      </el-col>
    </el-row>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: "pos",
  data() {
    return {
      tableData: [
        {
          goodsName: "可口可乐",
          price: 8,
          count: 1
        },
        {
          goodsName: "香辣鸡腿堡",
          price: 15,
          count: 1
        },
        {
          goodsName: "爱心薯条",
          price: 8,
          count: 1
        },
        {
          goodsName: "甜筒",
          price: 8,
          count: 1
        }
      ],
      oftenGoods: [],
      type0Goods: [],
      type1Goods: [],
      type2Goods: [],
      type3Goods: [],
    };
  },
  created:function(){
    axios.get('http://jspang.com/DemoApi/oftenGoods.php')
    .then(response=>{
      console.log('response')
      // console.log(response)
      this.oftenGoods=response.data
    })
    .catch(error=>{
      console.log('error')
      // console.log(error)
    })

    axios.get('http://jspang.com/DemoApi/typeGoods.php')
    .then(response=>{
      console.log('response')
      // console.log(response)
      this.oftenGoods=response.data
    })
    .catch(error=>{
      console.log('error')
      // console.log(error)
    })
  },
  mounted: function() {
    //在所有虚拟dom加载完成后执行
    var orderHeight = document.body.clientWidth;
    document.getElementById("order-list").style.height = orderHeight + "px";
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.pos {
  font-size: 12px;
}
.pos-order {
  background-color: #f9fafc;
  border-right: 1px solid #c0ccda;
}
.order-tabs {
  padding: 0 15px;
  font-size: 20px;
}
.order-btn {
  margin-top: 10px;
  text-align: center;
}
.title {
  height: 20px;
  border-bottom: 1px solid #d3dce6;
  background-color: #f9fafc;
  padding: 10px;
  text-align: left;
}
.often-goods-list ul li {
  list-style: none;
  float: left;
  border: 1px solid #e5e9f2;
  padding: 10px;
  margin: 10px;
  background-color: #fff;
}
.o-price {
  color: #58d7ff;
}
.goods-type {
  clear: both;
}
.cookList li {
  list-style: none;
  width: 23%;
  border: 1px solid #e5e9f2;
  height: auto;
  overflow: hidden;
  background-color: #fff;
  padding: 2px;
  float: left;
  margin: 2px;
}
.cookList li span {
  display: block;
  float: left;
}
.foodImg {
  width: 40%;
}
.foodName {
  font-size: 18px;
  padding-left: 10px;
  color: brown;
}
.foodPrice {
  font-size: 16px;
  padding-left: 10px;
  padding-top: 10px;
}
</style>
