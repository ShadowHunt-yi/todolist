<template>
    <li>
        <label>
            <input type="checkbox" :checked="n.done" @click="change(n.id)"/>
            <span>{{n.title}}</span>
        </label>
        <button class="btn btn-danger" @click="deletetodo(n.id)">删除</button>
    </li>
</template>

<script>
export default {
    name: 'Item',
    props:[
        'todos',
        'changeCheck',
        'moveTodo',
        'n',
    ],
    methods: {
        //改变选择状态
        change(id){
            // this.changeCheck(id);
            this.$bus.$emit('changeCheck',id)
        },
        //删除一个todo
        deletetodo(id){
            if(confirm('确定删除？')){
                // this.moveTodo(id)
                this.$bus.$emit('moveTodo',id)
            }
        },
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
li :hover  button{
    display: block;
}
</style>