<template>
    <div class="todo-footer" v-show="todos.length">
        <label>
            <input type="checkbox" :checked="doneTotal == todos.length" @change="checkout" />
        </label>
        <span>
            <span>已完成{{ doneTotal }} </span> / 全部{{ todos.length }}
        </span>
        <button class="btn btn-danger" @click="clearTodo">清除已完成任务</button>
    </div>
</template>

<script>

export default {
    name: 'Drop',
    props: [
        'todos',
        'checkAll',
        'clearAll'
    ],
    computed: {
        //计算有几个已完成
        doneTotal() {
            return this.todos.reduce((pre, todo) => pre + (todo.done ? 1 : 0), 0)
        }
    },
    methods: {
        //全选或全不选
        checkout(e) {
            this.checkAll(e.target.checked)
        },
        //清除全部选择
        clearTodo(todos){
            this.clearAll(todos)
        }

    }

}  
</script>

<style scope>
/*footer*/
.todo-footer {
    height: 40px;
    line-height: 40px;
    padding-left: 6px;
    margin-top: 5px;
}

.todo-footer label {
    display: inline-block;
    margin-right: 20px;
    cursor: pointer;
}

.todo-footer label input {
    position: relative;
    top: -1px;
    vertical-align: middle;
    margin-right: 5px;
}

.todo-footer button {
    float: right;
    margin-top: 5px;
}
</style>