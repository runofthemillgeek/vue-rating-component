<template>
  <div id="app">
    <app-home />
  </div>
</template>

<script>
import AppComponent from './components/home';

export default {
  name: 'app',
  components: {
    'app-home': AppComponent
  }
}
</script>

<style>
  @import '~bootstrap/dist/css/bootstrap.min.css';
</style>
