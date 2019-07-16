<template>
    <section>
        <transition-g>
            <li v-for="(todoItem,index) in propsdata" class="shadow" v-bind:key="todoItem">
                <i class="checkBtn fas fa-check" aria-hidden="true"></i>
                {{ todoItem }}
                <modals-container />
                <span class="updateBtn" type="button" @click="updateTodo(todoItem, index)">
                    <i  class="far fa-paper-plane" aria-hidden="true"></i>
                </span>	

                <span class="removeBtn" type="button" @click="removeTodo(todoItem, index)">
                    <i class="far fa-trash-alt" aria-hidden="true"></i>
                </span>	
            </li>
        </transition-g>
        
        <modal v-if="showModal" @close="showModal = false">
            <h3 slot="header">내용을 수정해주세요!</h3>
            <span slot="body">
                <input type="text" >
            </span>
            <span slot="footer" @click="showModal=false">
                <i class="far fa-paper-plane" aria-hidden="true"></i>
            </span>
        </modal>

    </section>
</template>

<script>
import Modal from './common/Modal.vue'




export default {
    props: ['propsdata'],
    data(){
        return{
            showModal:false,  //모달 동작을 위한 플래그 값
            loginType:false
        }
    },
    mounted(){
        this.doc_del_rendar();
    },
    methods: {
        removeTodo(todoItem, index){
            this.$emit('removeTodo',todoItem, index);
        },
        updateTodo(){
            this.showModal = !this.showModal;
        }
    },
    components:{
        Modal: Modal
    }
}
</script>


<style>
ul{
    list-style-type: none;
    padding-left:  0px;
    margin-top: 0;
    text-align:  left;
}

li {
    display: flex;
    min-height: 50px;
    height: 50px;
    line-height: 50px;
    margin: 0.5rem 0;
    padding : 0 0.9rem;
    background: white;
    border-radius: 5px;
}

.checkBtn {
    line-height: 45px;
    color: #62acde;
    margin-right: 5px;
}

.removeBtn{
    align-content: right;
    margin-left: 15px;
    color:#de4343;
}
.updateBtn{
    align-content: right;
    margin-left: auto;
    color: green;
}

</style>
