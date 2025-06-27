<script setup>
  import { ref  } from 'vue';
  import axios from 'axios';

  const url = ref('https://');  
  const title = ref('');  
  const urlList = ref([]);  

  const addUrl = () => {  
    if (url.value) {  
      urlList.value.push({ url: url.value, title: title.value });  
      url.value = 'https://';  
      title.value = '';  
      saveUrl();  
    }  
  };
  const saveUrl = () => {  
    localStorage.setItem('urlList', JSON.stringify(urlList.value));  
  };  
  const removeUrl = (index) => {  
    urlList.value.splice(index, 1);  
    saveUrl();  
  };    

  const clearUrl = () => {  
    urlList.value = [];  
    saveUrl();  
  };  
  

</script>

<template> 
<div class="px-4">  
  <h1 class="text-3xl mt-5">收藏網址⼩⼯具</h1>  
  <br>
  請輸入標題
  <input class="input" v-model="title" style="width:600px" />  
  <br><br>
  請輸入網址
  <input class="input" v-model="url" style="width:540px" />
  <button @click="addUrl" class="btn btn-warning btn-small ms-2">新增</button>
  <div class="mt-10 h-80 rounded-xl border-1 border-blue bg-white p-4 overflow-auto">
    <label class="mt-2"> 收藏清單 </label> <br>
    <lu>
      <li v-for="(x, index) in urlList" :key="index" class="mt-2 ms-3" >
        <button @click="removeUrl(index)" class="btn btn-soft btn-error btn-small ms-2">删除</button>  
        <a :href="x.url" target="_blank" class="link link-info  ms-2">{{ x.title }}</a> 
      
      </li>
    </lu>
  </div>
  <br>
  <button @click="clearUrl" class="btn btn-soft btn-info btn-small mt-3">清空全部</button>    
</div>
</template>

<style scoped></style>
