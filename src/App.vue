
<template>
  <div id="app" :class="(mode === 'dark') ? 'dark' : 'light'">
    <div class="container">
      <NavBar :mode="mode" @toggle="toggle"/>
      <div class="search-bar">
        <input type="text" placeholder="Search Github username ..." v-model="username" />
        <button type="submit" @click="getUserInfo" v-if="username" >Search</button>
      </div>
      <h3 v-if="!userExists" class="search-error">User does not exist...</h3>
      <div v-if="loading" class="loader"></div>
      <UserInfo v-if="userInfo && !loading && userExists" :userInfo="userInfo" />
    </div>
  </div>
</template>

<script>

import UserInfo from '@/components/UserInfo.vue'
import NavBar from '@/components/NavBar.vue'
import {ref} from 'vue';
import axios from 'axios';


export default {
  name: 'App',
  components: {
     UserInfo,
     NavBar
  },

  setup() {
    const username = ref("");
    const userInfo =  ref("");
    const loading = ref(false);
    const userExists = ref(true);
    const mode = ref('light');
    

  
    const getUserInfo = async () => {
      loading.value = true;
      try {
        const response = await axios.get(`https://api.github.com/users/${username.value}`);
        const result = response.data;
        userInfo.value = {
          image: result.avatar_url,
          name: result.name,
          user_name: result.login,
          joined: result.created_at,
          bio: result.bio,
          repos: result.public_repos,
          followers: result.followers,
          following: result.following,
          location: result.location,
          twitter: result.twitter_username,
          blog:result.blog,
          company: result.company
        }
        loading.value = false;
        userExists.value = true;
      } catch (error) {
        if(error.message === 'Network Error') {
          alert(error.message); 
        } else {
          userExists.value = false;
        }
      }
      username.value = '';
      loading.value = false;
    };

    const toggle = () => {
      if (mode.value === 'dark'){
        mode.value = 'light'
      } else {
        mode.value = 'dark'
      }
    }

    return {
      username,
      userInfo,
      loading,
      mode,
      userExists,
      getUserInfo, 
      toggle
    }
  }
}
</script>




