<template>
  <div>
    <div class="todo-container">
      <div class="todo-wrap">
        <Header :addlist="addlist"></Header>
        <List :changeTodo="changeTodo" 
        :todos="todos" 
        :removeli="removeli" 
       
       ></List>
        <Footer
        :todo="todos"
        :clearAllDone="clearAllDone"
        ></Footer>
      </div>
    </div>
  </div>
</template>

<script>
import Header from '@/components/Header.vue'
import List from '@/components/List.vue'
import Footer from '@/components/Footer.vue'
export default {
  name: 'App',
  components: {
    Header,
    List,
    Footer
  },
  data() {
    return {
      // todos: [
      //   { id: 1, title: 'THESHY', done: false },
      //   { id: 2, title: '小虎', done: true },
      //   { id: 3, title: 'gaola', done: true },
      //   { id: 4, title: '小明', done: true },
      // ]
      todos:JSON.parse(localStorage.getItem('todos'))||[]
    }

  },
  //数据在哪里更该 方法就在哪里
  methods: {
    addlist(val) {
      let flag = this.todos.some((item) => {
        return item.title === val.title
      })
      if (!flag) {
        this.todos.unshift(val)
      } else {
        alert('重复内容请重新输入')
      }
    },
    removeli(id) {
      this.todos = this.todos.filter((item) => item.id !== id)
    },
    changeTodo(id) {
      this.todos.forEach(item => {
        if (item.id == id) item.done = !item.done
      });
    },
      // 清除已完成的
    clearAllDone(){
      this.todos = this.todos.filter(item=>!item.done)
    }
  },
  wath: {
    todos: {
      handler(newval, loaval) {
        localStorage.setItem('todos',JSON.stringify(this.todos))
      }
    }
  }

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
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2),
    0 1px 2px rgba(0, 0, 0, 0.05);
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
</style>
