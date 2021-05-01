<template>
  <div>
    <input
      id='search'
      autofocus
      type="search"
      :disabled="isFetchingData"
      :placeholder="description"
      @keyup.enter="onEnter($event.target.value)"
    />
  </div>
</template>

<script>
export default {
  name: 'search',
  props: {
    description: String,
    onEnter: Function,
    isFetchingData: Boolean,
  },
};
</script>

<style scoped>
#search {
  width: 100%;
  margin-bottom: 10px;
  font-size: 1.2em;
}
</style>
