<template>
  <div class="container">
    <h1>Memo</h1>
    <Container/>
  </div>
</template>

<script>
import Container from './components/Container.vue'

export default {
  components: {
    Container
  }
}

</script>

<style>
.container {
  width: 50%;
  margin: 0 auto;
}
</style>
