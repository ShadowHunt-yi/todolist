<template>
    <li>
        <label>
            <input type="checkbox" :checked="todo.done" @click="change(todo.id)" />
            <span v-show="!todo.isEdit">{{ todo.title }}</span>
            <input type="text" 
            v-show="todo.isEdit" 
            :value="todo.title"
            @blur="ItemBlur(todo,$event)"
            ref="inputTitle" 
            @keyup.enter="alter(todo,$event)"
            />
        </label>
        <button class="btn btn-danger" @click="deletetodo(todo.id)">删除</button>
        <button v-show="!todo.isEdit" class="btn btn-Edit" @click="EditTodo(todo)">编辑</button>
    </li>
</template>

<script>
export default {
    name: 'Item',
    props: [
        'todo'
    ],
    methods: {
        //改变选择状态
        change(id) {
            // this.changeCheck(id);
            this.$bus.$emit('changeCheck', id)
        },
        //删除一个todo
        deletetodo(id) {
            if (confirm('确定删除？')) {
                // this.moveTodo(id)
                this.$bus.$emit('moveTodo', id)
            }
        },
        //修改每项todo的内容
        EditTodo() {
            this.todo.isEdit = true;
            //定时器依然能完成这个工作
            // setTimeout(() => {
            //     this.$refs.inputTitle.focus()
            // });
            //nextTick会在dom解析完成后进行回调
            this.$nextTick(function(){
                //当点击编辑后将焦点转到输入框
                this.$refs.inputTitle.focus()
            })
        },
        //当输入框失去焦点时会调用
        ItemBlur(todo,e) {
            this.todo.isEdit = false;
            //判断修改数据是否为空
            if(e.target.value!=''){ 
                this.$bus.$emit('updateTodo',todo.id, e.target.value)
            }else{
                alert("不能修改为空")
            }
        },
        alter(todo,e){
            this.todo.isEdit = false;
            //判断修改数据是否为空
            if(e.target.value!=''){ 
                this.$bus.$emit('updateTodo',todo.id, e.target.value)
            }else{
                alert("不能修改为空")
            }
        }
    },

}
</script>

<style scope>
/*item*/
li {
    list-style: none;
    height: 36px;
    line-height: 36px;
    padding: 0 5px;
    border-bottom: 1px solid #ddd;
}

li label {
    float: left;
    cursor: pointer;
}

li label li input {
    vertical-align: middle;
    margin-right: 6px;
    position: relative;
    top: -1px;
}

li button {
    float: right;
    display: none;
    margin-top: 3px;
}

li:before {
    content: initial;
}

li:last-child {
    border-bottom: none;
}

li:hover {
    background-color: #ddd;
}

li:hover button {
    display: block;
}
</style>