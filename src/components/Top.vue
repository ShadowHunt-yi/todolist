<template>
    <div class="todo-header">
        <input type="text" placeholder="请输入你的任务名称，按回车键确认" v-model="title" @keyup.enter="add" />
    </div>
</template>

<script>
import  {nanoid} from 'nanoid'
export default {
    name: 'Top',
    props:[
        'receive'
    ],
    data() {
        return {
            title:''
        }
    },
    methods: {
        add(e){
            //静止为空输入
            if(this.title==''){return alert('请输入有效事件')}
            //将输入的值包装成todos对象
           const a = {id:nanoid(),title:e.target.value,done:false};
           //将对象传回app组件进行处理 
           this.receive(a);   
            //清空输入
            this.title=''

            
        }
    },
}
</script>

<style scope>
.todo-header input {
  width: 560px;
  height: 28px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 7px;
}

.todo-header input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
}

</style>