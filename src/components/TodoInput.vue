<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" placeholder="Type what you have to do" v-on:keyup.enter="addTodo">
        <span class="addContainer" @click="addTodo">
            <i class="addBtn fas fa-plus" aria-hidden="true"></i>
        </span>
        
        <modal v-if="showModal" @close="showModal = false">
            <h3 slot="header">경고</h3>
            <h5 slot="body"> 할 일을 입력하세요.</h5>
            <span slot="footer" @click="showModal=false">
               
                <i class="closeModalBtn fas fa-times" aria-hidden="true"></i>
            </span>
        </modal>
    </div>
</template>

<script>
import Modal from './common/Modal.vue'
export default {
    data(){
        return{
            newTodoItem:'',
            showModal:false  //모달 동작을 위한 플래그 값
        }
    },
    methods:{
        addTodo(){
            if(this.newTodoItem !==""){
                var value= this.newTodoItem && this.newTodoItem.trim();
                this.$emit('addTodo',value); // 상위 컴포넌트(App.vue)로 이벤트 보냄
                this.clearInput();  //input에 입력 완료 후 input 비우기
            }else{
                this.showModal = !this.showModal;
            }
        },
        clearInput(){
            this.newTodoItem='';
        }
    },
    components:{
        Modal: Modal
    }
}
</script>

<style scoped>
    input:focus{
        outline: none;
    }
    .inputBox{
        background: white;
        height: 50px;
        line-height: 50px;
        border-radius: 5px;
    }
    .inputBox input {
        border-style:none;
        font-size: 0.9rem;
    }
    .addContainer {
        float: right;
        background: linear-gradient(to right, #6478FB, #8763FB);
        display: block;
        width: 3rem;
        border-radius: 0 5px 5px 0;

    }
    .addBtn{
        color:white;
        vertical-align: middle;
    }
</style>
