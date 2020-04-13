<template>
    <div class="searchWrapper">

      <input
      type="text" name="search"
      v-model="searchValue"
      @input="handleInput">
    </div>
</template>

<script>
export default {
  name: 'SearchInput',
};
</script>

<style lang="scss" scoped>
    .searchWrapper{
    display: flex;
    flex-direction: column;
    width: 300px;
  }

  input{
    height: 30px;
    border: 0;
    border-bottom: 1px solid black;
  }
</style>
