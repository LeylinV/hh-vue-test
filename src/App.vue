<template>
  <div id="app">
    <HeaderUI/>
    <div class="page">
      <UsersTablePage/>
    </div>
    <FooterUI/>
  </div>
</template>

<script>
import HeaderUI from "./components/ui/HeaderUI/HeaderUI.vue";
import FooterUI from "./components/ui/FooterUI/FooterUI.vue";
import UsersTablePage from "./components/UsersTablePage.vue";

export default {
  name: 'App',
  components: {
    UsersTablePage,
    FooterUI,
    HeaderUI,
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');
* {
  padding: 0;
  margin: 0;
  font-family: 'Montserrat', sans-serif;
}

*,
*::before,
*::after {
  box-sizing: border-box;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}
.page {
  flex: 1;
  width: 100%;
  max-width: 900px;
  margin: 10px auto;
}
</style>
