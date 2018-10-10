<template>
<div class="container">
  <app-header></app-header>
  <hr />
  <server-content></server-content>
  <hr />
  <app-footer></app-footer>
</div>
</template>

<script>
import Header from './components/shared/header';
import Content from './components/server/content';
import Sidebar from './components/server/sidebar';
import Footer from './components/shared/footer';

export default {
  components: {
      'app-header': Header,
      'server-content': Content,
      'server-sidebar': Sidebar,
      'app-footer': Footer
  }
}
</script>

<style lang="scss">
</style>
