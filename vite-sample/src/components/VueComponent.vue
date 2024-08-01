<script setup>
import {ref}from 'vue';
const data =ref( [
  {
    "id": 1,
    "name": "珍珠奶茶",
    "description": "香濃奶茶搭配QQ珍珠",
    "price": 50,
    "stock": 20,
    "Flag":false
  },
  {
    "id": 2,
    "name": "冬瓜檸檬",
    "description": "清新冬瓜配上新鮮檸檬",
    "price": 45,
    "stock": 15,
    "Flag":false
  },
  {
    "id": 3,
    "name": "翡翠檸檬",
    "description": "綠茶與檸檬的完美結合",
    "price": 55,
    "stock": 30,
    "Flag":false
  },
  {
    "id": 4,
    "name": "四季春茶",
    "description": "香醇四季春茶，回甘無比",
    "price": 45,
    "stock": 10,
    "Flag":false
  },
  {
    "id": 5,
    "name": "阿薩姆奶茶",
    "description": "阿薩姆紅茶搭配香醇鮮奶",
    "price": 50,
    "stock": 25,
    "Flag":false
  },
  {
    "id": 6,
    "name": "檸檬冰茶",
    "description": "檸檬與冰茶的清新組合",
    "price": 45,
    "stock": 20,
    "Flag":false
  },
  {
    "id": 7,
    "name": "芒果綠茶",
    "description": "芒果與綠茶的獨特風味",
    "price": 55,
    "stock": 18,
    "Flag":false
  },
  {
    "id": 8,
    "name": "抹茶拿鐵",
    "description": "抹茶與鮮奶的絕配",
    "price": 60,
    "stock": 20,
    "Flag":false
  }
]);
const dataTemp=ref([ 
  {
    "id": "",
    "name": "",
    "description": "",
    "price": "",
    "stock": "",
    "Flag":false
  } ]);
function Drink(id,stock){
    data.value=data.value.map((item) => {
    if (item.id === id) {
      item.stock = stock;
    }
    return item
});
}
function toggleFlag(id,Flag){
    data.value=data.value.map((item) => {
    if (item.id === id) {
      item.Flag = Flag;
    }
    return item
});
}
function Contact(id){
  data.value=data.value.map((item) => {
    if (item.id === id) {
      item.name =  dataTemp.value.name;
      item.Flag = !item.Flag ;
    }
    return item
});
// data.value[id]= dataTemp.value;
}
const dataEdit=(data,id,Flag)=>{
  toggleFlag(id,Flag);
  dataTemp.value={...data};
}
</script>
<template>
    
<div class="box">
  <div class="top">
    <h1 class="name">餐點管理工具
    </h1>
  </div>
  <div class="bottom">
    <table >
      <thead class="nav">
        <tr>
          <th scope="col">品項</th>
          <th scope="col">描述</th>
          <th scope="col">價格</th>
          <th scope="col">庫存</th>
          <th scope="col">修改品項</th>
        </tr>
      </thead>
      <tbody class="text">
        <tr v-for="item in data" :key="item.id">
          <td v-if=" !item.Flag">{{ item.name }}</td>
          <td v-if=" item.Flag">
            <input type="text" v-model="dataTemp.name" />
            <button  class="btn btnyes" @click="Contact(item.id)" :disabled="item.stock < 1">確認</button>            
            <button  class="btn btnno"  @click="toggleFlag(item.id,!item.Flag)" >取消</button>
          </td>
          <td><small>{{ item.description }}</small></td>
          <td>{{ item.price }}</td>
          <td>
            <button  class="btn btnWebsite" @click="Drink(item.id, item.stock - 1)" :disabled="item.stock < 1">-</button>
            {{ item.stock }}
            <button class="btn btnWebsite" @click="Drink(item.id, item.stock + 1)">+</button>
          </td>
          <td style="text-align: center;">
            <button  class="btn btnWebsite"  @click="dataEdit(item,item.id,!item.Flag)" >編輯</button>
          </td>
        </tr>
      </tbody>
    </table>

  </div>
</div>
</template>
<style >
*{
  font-family:微軟正黑體;
}
html,body{
  background-color: #D4D0BE;
  width:100%;
  height:100%;
  margin: 0;
  display:flex;
  justify-content:center;
  align-items:center;  
  font-size: 14px;
}
a{color:initial;
  text-decoration:initial;
}
.box{
  width:max-content;
  background-color: #fff;
  box-shadow:20px 20px 50px 0 rgba(0,0,0,0.5);
  
}
.box:hover{
  box-shadow:5px 5px  60px rgba(0,0,0,0.5);
}
.top{
    align-content: center;
  height:100px;
  position: relative;
  background-color: #52433D;
}
.top .name{
    position: absolute;
    display: flex;
    bottom: 0px;
    letter-spacing: 2px;
    color: white;
    font-weight: 300px;
    background: linear-gradient(transparent 0%, black 100%);
    width: 100%;
    box-sizing: border-box;
    padding-bottom: 32px;
    align-items: flex-end;
    justify-content: center;
}
.bottom{
  padding:10px 20px 20px 20px;
}
.bottom li{
  padding:5px 0px ;
}
.buttoms{
  margin-top: 30px;

}
.btnyes{
  
  background-color: #bed4c2;
  transition:0.5s;
}
.btnyes:hover{
  background-color: #ffffff;;
}
.btnno{
  
  background-color: #d4bebe;
  transition:0.5s;
}
.btnno:hover{
  background-color: #ffffff;;
}
.btnWebsite{
  background-color: #D4D0BE;
  transition:0.5s;
  }
.btnWebsite:hover{
  background-color: #f2e9c4;;
}
.nav {
    background-color: #a19c85;
    color: #FFFFFF;
    justify-content: center;
    align-items: center;
    letter-spacing: 1px;
    }
    .text {
    width: 100%;
    height: 100%;
}
</style>