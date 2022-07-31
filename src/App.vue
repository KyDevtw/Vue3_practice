<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import { def } from '@vue/shared';
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <div id="myApp">
    @{{user.username}} - {{fullName}}
    <strong>Followers:</strong>{{followers}}
    <button @click="followUser" style="background: grey; color: white; border-width: 0px;">
      Follow
    </button>
  </div>
</template>

<script>

export default {
  name: "App",
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
      }
    }
  },
  watch: {
    // name the function after the data that you want to watch
    // can be data and computed ex. when the fullName() changes, trigger the watch function
    followers(newFollowerCount, oldFollowerCount) {
      if(oldFollowerCount < newFollowerCount){
        console.log(`${this.user.username} has gained a follwer!`);
      }
    }
  },
  // functions 寫在這裡 () => void
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    }
  },
  // functions 寫在這裡 () => return
  methods: {
    followUser() {
      this.followers++;
      // this.followers = this.followers + 1;
      // this.followers += 1;
    }
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
