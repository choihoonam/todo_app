<template>
  <section>
    <transition-group name="list" tag="ul">
      <li v-for="(todoItem,index) in propsdata" :key="todoItem.item" class="shadow">
        <i class="checkBtn fas fa-check" v-bind:class="{checkBtnCompleted:todoItem.completed}" v-on:click="toggleComplete(todoItem,index)"></i>
        <span v-bind:class="{textCompleted:todoItem.completed}">{{ todoItem.item }}</span>
        <span class="removeBtn" type="button" @click="removeTodo(todoItem,index)">
          <i class="fas fa-trash-alt"></i>
        </span>
      </li>
    </transition-group>
  </section>
</template>

<script>
export default {
  props: ['propsdata'],
  
  methods: {
    removeTodo(todoItem,index){
      this.$emit('removeTodo',todoItem,index);
    },
    toggleComplete: function(todoItem,index){
      this.$emit('toggleItem', todoItem);
    }
  },
}
</script>

<style scope>
  ul {margin-top:0; padding-left:0; list-style-type:none; text-align:left;}
  li {display:flex; height:50px; min-height:50px; margin:0.5rem 0; padding:0 0.9rem; border-radius:5px; line-height:50px; background-color:white;}
  .checkBtn {margin-right:5px; color:#62acde; line-height:50px;}
  .removeBtn {margin-left:auto; color:#de434d;}

  .checkBtnCompleted {color:#b3adad;}
  .textCompleted {color:#b3adad; text-decoration:line-through;}

  .list-enter-active, .list-leave-active {transition:all 1s;}
  .list-enter, .list-leave-to {opacity:0; transform:translateY(30px);}
</style>
