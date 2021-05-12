<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" placeholder="Type what you have to do" v-on:keyup.enter="addTodo">
        <span class="addContainer" v-on:click="addTodo">
            <i class="addBtn fas fa-plus" arial-hidden="true"></i>
        </span>
        <!-- use the modal component, pass in the prop -->
      <Modal v-if="showModal" @close="showModal = false">
        <!--
      you can use custom content here to overwrite
      default content
    -->
        <h3 slot="header">custom header</h3>
      </Modal>

    </div>
</template>

<script>
import Modal from './common/Modal.vue'

export default {
    data() {
        return {
            newTodoItem:'',
            showModal: false
        }
    },

    methods: {
        addTodo() {
            if( this.newTodoItem !== "") {
                var value = this.newTodoItem && this.newTodoItem.trim();
                this.$emit('addTodo', value);
                this.clearInput();
            }
        },
            
        clearInput() {
                this.newTodoItem = '';
        }
    },

    components: {
        Modal: Modal
    }
}
</script>

<style scoped>
    input:focus {
        outline: none,
    }

    .inputBox {
        background: whie;
        height: 50px;
        line-height: 50px;
        border-radius: 5px;
    }


    .inputBox input {
        border-style: none;
        font-size: 0.9rem;
    }

    .addContainer {
        float: right;
        background: linear-gradient(to right, #6478FB, #8763FB);
        display: block;
        width:  3rem;
        border-radius: 0 5px 5px 0;
    }
    .addBtn {
        color: white;
        vertical-align: middle;
    }

</style>