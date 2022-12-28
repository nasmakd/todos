<template>
  <div class="clearAllContainer">
    <span class="clearAllBtn" v-on:click="clearTodo">Clear All</span>
  </div>
</template>

<script>
export default {
  methods: {
    clearTodo(){
      this.$emit("removeAll")
    }
  }
}
</script>

<style scoped>
  .clearAllBtn{
    display: inline-block;
    margin-top: 10px;
    padding: 8px 18px;
    border: 1px solid   #3C6255;
    border-radius: 8px;
    color: #3C6255;
    cursor: pointer;
    transition: .5s;
  }
  .clearAllBtn:hover{
    background-color: #3C6255;
    color: #fff;
  }
</style>