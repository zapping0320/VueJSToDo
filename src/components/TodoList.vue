<template>
    <section>
        <transition-group name="list" tag="ul">
            <li v-for="(todoItem, index) in propsdata" :key="todoItem.item" class="shadow">
                <i class="checkBtn fas fa-check" v-bind:class="{checkBtnCompleted: todoItem.completed}" aria-hidden="true" 
                v-on:click="toggleComplete(todoItem, index)"></i>
                <span v-bind:class="{textCompleted: todoItem.completed}">{{ todoItem.item }}</span>
                <span class="removeBtn" type="button" @click="removeTodo(todoItem, index)">
                    <i class="far fa-trash-alt" aria-hidden="true"></i>
                </span>
            </li>
        </transition-group>
    </section>
</template>

<script>
export default {
    props: ['propsdata'],

    methods :{
        removeTodo(todoItem, index){
            this.$emit('removeTodo', todoItem, index);
        },
        toggleComplete : function(todoItem, index){
            this.$emit('toggleItem', todoItem, index);
        }
    }
}
</script>

<style scoped>
   

    ul {
        list-style-type: none;
        padding-left: 0px;
        margin-top: 0;
        text-align: left;
    }

    li {
        display: flex;
        min-height: 50px;
        height: 50px;
        line-height: 50px;
        margin: 0.5rem 0;
        padding: 0 0.9rem;
        background: white;
        border-radius: 5px;
    }

    .removeBtn {
        margin-left: auto;
        color: #de4343;
    }

    .checkBtn {
        line-height: 45px;
        color:  #62acde;
        margin-right: 5px;
    }

    .checkBtnCompleted {
        color: #b3adad;
    }

    .textCompleted {
        text-decoration: line-through;
        color: #b3adad;
    }
   

    .list-enter-active, .list-leave-active {
        transition: all 1s;
    }
    .list-enter, .list-leave-to {
        opacity: 0 ;
        transform: translate(30px);
    }
</style>