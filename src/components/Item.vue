<template>
    <li @mouseover="todolis=true" @mouseout="todolis=false" :class="{ active:todolis}">
      <label>
        <input type="checkbox" @change="changeli" />
        <span>{{todo.title}}</span>
      </label>
      <button class="btn btn-danger"
       v-show="todolis"
       @click="removelis"
       >删除</button>
    </li>
</template>

<script>
export default {
  name: 'Item',
  props: ['todo','removeli','changeTodo',],
  data() {
    return {
    todolis:false
  }
  },
  methods: {
    removelis() {
   this.removeli(this.todo.id)

    },
    changeli() {
     this.changeTodo(this.todo.id)
    },
   
 }
  
}
</script>

<style scoped>
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
  /*display: none;*/
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}
li.active{

  background-color: #ccc;
}
</style>
