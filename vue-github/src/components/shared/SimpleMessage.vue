<template>
  <div id="divStyle">
    <p id="message">{{ message }}</p>
  </div>
</template>

<script>
export default {
  props: {
    message: String
  }
}
</script>

<style scoped>
#divStyle {
  padding-top: 20px;
}

#message {
  font-weight: bold;
  font-size: 1.1em;
  text-align: center;
}
</style>




