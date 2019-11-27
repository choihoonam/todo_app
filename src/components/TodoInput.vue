<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" placeholder="Type what you have to do" v-on:keyup.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo">
      <i class="addBtn fas fa-plus" aria-hidden="true"></i>
    </span>

    <modal v-if="showModal" @close="showModal = false">
      <h3 slot="header">경고</h3>
      <span slot="footer">
        할 일을 입력하세요.
        <i class="closeModalBtn fas fa-times" aria-hidden="true" @click="showModal = false"></i>
      </span>
    </modal>
  </div>
</template>

<script>
import Modal from './common/Modal.vue'

export default {
  data() {
    return {
      newTodoItem: "",
      showModal: false
    };
  },
  methods: {
    addTodo() {
      if (this.newTodoItem !== "") {
        this.$emit('addTodoItem',this.newTodoItem);
        this.clearInput();
      }else{
        this.showModal = !this.showModal;
      }
    },
    clearInput(){
      this.newTodoItem = '';
    }
  },
  components: {
    Modal
  }
  
};
</script>

<style scope>
  input:focus {outline:none;}
  .inputBox {height:50px; border-radius:5px; line-height:50px; background:white;}
  .inputBox input {border:none; font-size:0.9rem;}
  .addContainer {float:right; width:3rem; border-radius:0 5px 5px 0; background:linear-gradient(to right,#3145fb,#8763fb);}
  .addBtn {color:white;}
</style>
