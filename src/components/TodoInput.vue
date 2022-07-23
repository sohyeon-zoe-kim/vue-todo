<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" @keyup.enter="addTodo()"/>
        <span class="addContainer" @click="addTodo">
            <i class="fa-solid fa-plus addBtn"></i>
        </span>
        <ModalView v-if="showModal">
            <h3 slot="header">
                경고!
                <i class="closeModalBtn fas fa-times" @click="showModal = false"></i>
            </h3>
            <div slot="body">무언가를 입력하세요.</div>
            <!-- <div slot="footer">@sohyeon.kim</div> -->
        </ModalView>
    </div>
</template>
<script>
import ModalView from './common/ModalView.vue';
export default {
    data : function(){
        return {
            newTodoItem: '',
            showModal: false
        }
    },
    components: {
        ModalView: ModalView
    },
    methods: {
        addTodo: function(){
            if(this.newTodoItem !== ''){
                this.$store.commit('addOneItem', this.newTodoItem);
                this.clearInput();
            }else{
                this.showModal = !this.showModal;
            }
        },
        clearInput: function(){
            this.newTodoItem = '';
        }
    },
}
</script>
<style scoped>
input:focus{
    outline:none;
}
.inputBox{
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
}
.inputBox input{
    height: 40px;
    width: 80%;
    border-style: none;
    font-size: 0.9rem;
}
.addContainer {
    float: right;
    background: linear-gradient(to right, #6478FB, #8763FB);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
}
.addBtn {
    color: white;
    width: 50px;
    vertical-align: middle;
}
</style>