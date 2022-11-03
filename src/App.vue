<template>
  <div id="root">
  <div class="todo-container">
    <div class="todo-wrap">
      <Top :receive="receive"/>
      <List :todos="todos" :changeCheck="changeCheck" :moveTodo="moveTodo"/>
      <Drop :todos="todos" :checkAll="checkAll" :clearAll="clearAll"/>
    </div>
  </div>
</div>
</template>

<script>
import Top from './components/Top.vue';
import List from './components/List.vue';
import Drop from './components/Drop.vue';

export default {
  name: 'App',
  components: {
    List,
    Top,
    Drop
  },
  data() {
        return {
            todos:[
          {id:'001',title:"eat",done:true}
        ]
        }
    },
    methods: {
      //收到一个对象并加入数组
      receive(x){
        //将top传来的对象加入todos首项
        this.todos.unshift(x)
      },
      //勾选事件
      changeCheck(id){
        this.todos.forEach((todo)=>{
          if(todo.id==id)todo.done=!todo.done
        })
      },
      //移除todo
      moveTodo(id){
        this.todos=this.todos.filter(
          todo =>todo.id!== id
        )
      },
      //全选或全不选
      checkAll(done){
        this.todos.forEach((todo)=>{
          todo.done=done;
        })
      },
      //清除全部选择
      clearAll(done){
        //过滤
        this.todos=this.todos.filter(
          todo =>!todo.done
        )
      }
      
    },
}
</script>

<style>
/*base*/
body {
  background: #fff;
}

.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}

.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}

.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}

.btn:focus {
  outline: none;
}

.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}

/*header*/



</style>
