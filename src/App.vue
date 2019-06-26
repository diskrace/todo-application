<template>
  <div>
    <todo-header></todo-header>
    <todo-input
      v-on:add="addTodoItem"
    ></todo-input>
    <todo-list
      v-bind:todolist="todoItems"
      v-on:remove="removeTodoItem"
      ></todo-list>
    <todo-footer
      v-on:clearall="removeAllItems"
    ></todo-footer>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue';
import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';
import TodoFooter from './components/TodoFooter.vue';

export default {
  components: {
    'todo-header': TodoHeader,
    'todo-input': TodoInput,
    'todo-list': TodoList,
    'todo-footer': TodoFooter
  },
  data() {
    return {
      todoItems: []
    };
  },
  methods: {
     fetchTodoItems: function() {
        //브라우저 저장소의 데이터를 불러오기
        for(var i = 0; i < localStorage.length; i++) {
            var item = localStorage.key(i);
            this.todoItems.push(item);
        }
    },
    addTodoItem: function(value) {
      // 배열에 추가
      this.todoItems.push(value);
      // 저장소에 저장
      localStorage.setItem(value, value);
    },
    removeAllItems: function() {
      this.todoItems = [];
      localStorage.clear();
    },
    removeTodoItem: function(todo, index) {
      this.todoItems.splice(index, 1);
      // 브라우저 저장소의 데이터 삭제
      localStorage.removeItem(todo);
    }
  },
  // 컴포넌트가 생성되자마자 실행되는 로직
  created: function() {
      this.fetchTodoItems();
  },
}
</script>

<style>

</style>
