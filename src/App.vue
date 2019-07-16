<template>
  <div id="app">
      <TodoHeader></TodoHeader>
      <TodoInput v-on:addTodo="addTodo"></TodoInput>
      <TodoList v-on:removeTodo="removeTodo" v-bind:propsdata="todoItems"></TodoList>
      <TodoFooter v-on:removeAll="clearAll"></TodoFooter>

  </div>
</template>

<script>
import TodoHeader from './components/ToodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'


export default {
  data(){
    return{
      todoItems: []
    }
  },
  created() {
        if(localStorage.length >0){
            for(var i=0; i<localStorage.length; i++){
                this.todoItems.push(localStorage.key(i));
            }
        }
    },
  methods:{
    addTodo(todoItem){
      //로컬 스토리지에 데이터를 추가하는 로직
      localStorage.setItem(todoItem,todoItem);
      this.todoItems.push(todoItem);
    },
    clearAll(){
      localStorage.clear();
      this.todoItems=[];
    },
    removeTodo(todoItem, index){
        localStorage.removeItem(todoItem);  //localstorage에 있는 아이템 삭제
        this.todoItems.splice(index,1)      // 배열에 정의한 아이템 삭제
        //console.log(todoItem,index);
    }
  }, 
  components:{
    'TodoHeader' : TodoHeader,
    'TodoInput' : TodoInput,
    'TodoList' : TodoList,
    'TodoFooter' : TodoFooter,
   
  },
}
</script>

<style>
body {
    text-align: center;
    background-color: #F6F6F8;
}
input{
    border-style: groove;
    width: 200px;
}
button{
    border-style: groove;
}
.shadow{
    box-shadow: 5px 10px 10px rgba(0,0,0,0.03)
}
</style>
