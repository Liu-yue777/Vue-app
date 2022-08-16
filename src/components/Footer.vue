<template>
  <div>
    <div class="todo-footer">
      <label>
        <input type="checkbox" v-model="isCheck"/>
      </label>
      <span> <span>已完成{{isDoneNum}}</span> / 全部{{todo.length}} </span>
      <button class="btn btn-danger" @click="clearAllDone">清除已完成任务</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Footer',
  props:['clearAllDone','todo'],
  // methods:{
  //   handleClear(){
  //     // 通知App把选中的数据清除掉
  //     this.clearAllDone()
  //   }
  // }
  computed:{
    isDoneNum(){
      return this.todo.filter(item=>{
        return item.done
      }).length
    },
    isCheck:{
      get(){
        return this.todo.every(item=>item.done)
      },
      set(value){
        // 根据现在全选的按钮的数据 修改列表项当中done的值
        this.todo.forEach(item=>{
          item.done = value
        })
      }
    }
  }
}
</script>

<style scoped>
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