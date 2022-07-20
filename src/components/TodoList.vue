<template>
    <div>
        <ul>
            <li :key="todoItem.item" v-for="(todoItem, index) in propsdata" class="shadow">
                <i class="fa-solid fa-check checkBtn" :class="{checkBtnCompleted: todoItem.completed}" @click="toggleComplete(todoItem,index)"></i>
                <span :class="{textCompleted: todoItem.completed}">{{todoItem.item}}</span>
                <span class="removeBtn" @click="removeTodo(todoItem,index)">
                    <i class="fa-solid fa-trash-can"></i>
                </span>
            </li>
        </ul>
    </div>
</template>
<script>
export default {
    props: ['propsdata'],
    methods: {
        removeTodo: function(todoItem,index){
            this.$emit('removeItem',todoItem, index);
        },
        toggleComplete: function(todoItem, index){
            this.$emit('toggleItem',todoItem, index);
        }
    }
}
</script>
<style scoped>
ul{
    list-style-type: none;
    padding-left: 0px;
    margin-top: 0;
    text-align: left;
}
li{
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
    color:#62acde;
    margin-right: 10px;
}
.checkBtnCompleted {
    color: #b3adad;
}
.textCompleted {
    text-decoration: line-through;
    color: #b3adad;
}
</style>