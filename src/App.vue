<script>
import SiteForm from './components/Form.vue';
import SitePreview from './components/Preview.vue';

const routes = {
  '/': SiteForm,
  '/preview': SitePreview
}

export default {
  name: 'App',
  data() {
    return {
      parent: {},
      children: [],
      currentPath: window.location.hash
    }
  },
  created() {
    let userInfo = localStorage.getItem('user-info');

    if (userInfo) {
      let userData = JSON.parse(userInfo);

      console.log(userData)

      this.parent = userData.parent;
      this.children = userData.children;
    }
  },
  computed: {
    currentView() {
      return routes[this.currentPath.slice(1) || '/'] || SitePreview;
    }
  },
  mounted() {
    window.addEventListener('hashchange', () => {
      this.currentPath = window.location.hash
    })
  }
}
</script>

<template>
  <div id="app">
    <div class="header">
      <div>
        <a href="/">
          <img src="./assets/logo-alef.png" alt="logo">
        </a>
      </div>
      <div class="header__menu">
        <a href="#/">Форма</a>
        <a href="#/preview">Превью</a>
      </div>
    </div>
    <div class="content">
      <component :is="currentView" :parent="parent" :children="children" />
    </div>
  </div>
</template>