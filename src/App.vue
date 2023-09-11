<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import { def } from '@vue/shared';
import { list } from 'postcss';
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <div id="myApp">
    @{{user.username}} - {{fullName}}
    <strong>Followers:</strong>{{followers}}
    <button @click="followUser" style="background: grey; color: white; border-width: 0px;">
      Follow
    </button>
    <!-- v-bind: can be replaced by : , used on element's key -->
    <a v-bind:href="link">v-bind功能</a>
    <ul>
      <!-- v-fro is similar to array for in function, key is required to use with it-->
      <!-- if the todo value is include an id, use :key="todo.id" to replace index -->
      <!-- this todo is the variable in v-for  -->
      <!-- index is can also display in the element -->
      <li v-for="(todo, index) in lists" :key="index"><input type="checkbox" :checked="todo.complete" />{{ index + 1 }}.{{
        todo.content }}</li>
    </ul>
    </div>
</template>

<script>

export default {
  name: "App",
  // data is a function return an object
  // null and undefine will retunr a empty value in DOM
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: "_Kurt",
        firstName: "Smith",
        lastName: "Henry",
        email: "kurtyang@blinbuy.com",
        isAdmin: true
      },
      link: "https://www.google.com/?client=safari",
      lists: [
        { complete: true, content: "項目1" },
        { complete: false, content: "項目2" },
        { complete: false, content: "項目3" },
        { complete: false, content: "項目4" },
        { complete: true, content: "項目5" }
      ]
    }
  },
  watch: {
    // name the function after the data that you want to watch
    // can be data and computed ex. when the fullName() changes, trigger the watch function
    // data 改變 dom 會重新 render, watch 是用來監聽給 js, 適合用在複雜或是異步操作
    // watch 函式名稱要與 data 中要監聽的資料名稱相同，data 值發生變化會自動調用 watch 內的同名函式執行
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} has gained a follwer!`);
      }
    }
  },
  // functions 寫在這裡 () => void
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
    // this 指到 Vue.createApp({}).mount('#app')，從 data 中獲取資料  
    // 將較於在 html 中寫的邏輯，寫在 computed 可以重複使用
    lable() {
      return this.showAnswer ? "隱藏" : "顯示"
    }
  },
  // functions 寫在這裡 () => return
  // method 常用在 vue 中的事件監聽 @click="methods()"
  methods: {
    followUser() {
      this.followers++;
      // this.followers = this.followers + 1;
      // this.followers += 1;
    },
    // 可以調動 data 資料
    toggleAnswer() { this.showAnswer = !this.showAnswer }
  },
  mounted() {
    //! like React useEffect
    this.followUser();
    console.log(this.user.firstName)
  }
}
</script>

<style lang="scss">
@import url(./style/_reset.scss);
#myApp {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  display: flex;
  flex-direction: column;
}
</style>
