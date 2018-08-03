<template>
  <div id="app">
    <h1>{{title}}</h1>
    <input v-model = "newTodo"  v-on:keyup.enter="addNew"> 
   <!--  这里的newItem就是输入框输入的东西 -->
    <ul class="list">
      <li v-for = "todo in todos" v-bind:class ="{finish:todo.isFinished}" v-on:click = "doThis(todo)" >
        {{todo.label}}
      </li>
    </ul>
    <h1>{{msg}}</h1>
<!--     <components-a></components-a> -->
  </div>
</template>

<script>
import Store from './store'
import componentsA from'./components/componentA'
// console.log(Store);
export default {
  name: 'App',
  components: {componentsA},  
  data () {
    return {
      title: 'This is my todo list',
      newTodo:'',
      todos:
      // {
      //   label:'coding',
      //   isFinished:false
      // },
      // {
      //   label:'walking',
      //   isFinished:true
      // }
      Store.fetch()
      
    }
  },
  watch:{//观看状态的变化
    todos:{
      handler:function(todos){
        // console.log(val,oldVal)
        Store.save(todos);
      },
      deep:true//有这个todos的状态被改才有用
    }
  },

  methods:{
    doThis:function(todo){
      todo.isFinished = !todo.isFinished
    },
    addNew:function(){
      this.todos.push({
      label:this.newTodo,
      isFinished:false
      })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 200px;
  position:relative;
}

.finish{
  text-decoration: line-through;
  color: #222;
/*  display:none;*/
}

.list{
  list-style: none;
  position:absolute;
  left:50%;
  margin-left:-140px;
}
.list li{
  width:200px;
  height:40px;
  background-color:#278392;
  margin-top:10px;
  font-size:20px;
  line-height:40px;
  color:#fff;
}
</style>
