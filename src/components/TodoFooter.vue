<template>
  <div class="clearAllContainer">
    <span class="clearAllBtn" @click="clearTodo">Clear All</span>
  </div>
</template>

<script>
export default {
  methods: {
    clearTodo(){
      this.$emit('removeAll');
    }
  },
};
</script>

<style>
  .clearAllContainer {width:8.5rem; height:50px; margin:0 auto; border-radius:5px; line-height:50px; background-color:white;}
  .clearAllBtn {display:block; color:#e20303;}
</style>
