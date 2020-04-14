<template>
    <div class="searchWrapper">

      <input
    id="search"
    name="search"
    :class="{ dark }"
    :value="value"
    @input="handleChange"
  />
    </div>
</template>

<script>
export default {
  name: 'SearchInput',
  props: {
    value: {
      type: String,
      required: true,
    },
    dark: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>
    .searchWrapper{
    display: flex;
    flex-direction: column;
    width: 250px;
    margin-top: 50px;
  }

  input{
    height: 30px;
    border: 0;
    border-bottom: 2px solid white;
    background: none;
    transition: box-shadow .5s easy-out;
    color: white;
    text-align: center;
    font-weight: 300;
    @media(min-width: 1024px){
      font-weight: 400;
    }
  }

  input:focus{
    outline: none;
    box-shadow: 0 5px 10px -8px rgba(255,255,255,.5);
  }

  .dark{
    color: black;
    border-bottom-color: black;
  }

  .dark:focus{
    box-shadow: 0 10px 20px -8px rgba(255,255,255,.5);
  }
</style>
