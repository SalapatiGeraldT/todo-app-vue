<script setup>
import CustomInput from "../components/CustomInput.vue";
import CustomButton from "../components/CustomButton.vue";
import { uid } from "uid";
import { ref, watch, computed } from "vue";
import TodoItem from "../components/TodoItem.vue";

const todoList = ref([]);

const todoCompleted = computed(() => {
  return todoList.value.every((todo) => todo.isCompleted);
});

watch(
  todoList,
  () => {
    setTodoListLocalStorage();
  },
  {
    deep: true,
  }
);

const fetchTodoList = () => {
  const savedTodoList = JSON.parse(localStorage.getItem("todoList"));
  if (savedTodoList) {
    todoList.value = savedTodoList;
  }
};
fetchTodoList();
const setTodoListLocalStorage = () => {
  localStorage.setItem("todoList", JSON.stringify(todoList.value));
};

const createTodo = (todo) => {
  todoList.value.push({
    id: uid(),
    todo,
    isCompleted: null,
    isEditing: null,
  });
};

const toggleTodoComplete = (todoIndex) => {
  todoList.value[todoIndex].isCompleted =
    !todoList.value[todoIndex].isCompleted;
};

const toggleEditTodo = (todoIndex) => {
  todoList.value[todoIndex].isEditing = !todoList.value[todoIndex].isEditing;
};
const updateTodo = (todoValue, todoIndex) => {
  todoList.value[todoIndex].todo = todoValue;
};

const deleteTodo = (todoIndex) => {
  if (window.confirm("Are You Sure?")) {
    todoList.value = todoList.value.filter((todo) => todo.id !== todoIndex);
  }
};
</script>

<template>
  <main class=" lg:mx-48 sm:mx-8 mx-0 px-4 ">
    <h1 class="pt-4 text-center text-2xl">Create Todo</h1>

    <CustomInput @create-todo="createTodo" />

    <ul v-if="todoList.length > 0">
      <TodoItem
        v-for="(todo, index) in todoList"
        
        :todo="todo"
        :index="index"


        @toggle-complete="toggleTodoComplete"
        @edit-todo="toggleEditTodo"
        @update-todo="updateTodo"
        @delete-todo="deleteTodo"
      />
    </ul>
    <div class="flex justify-center text-center text-violet-800">
      <span v-if="todoList.length === 0">Todo List Empty</span>
      <span v-if="todoCompleted && todoList.length > 0">
        Well Done! <br>Todo List Completed.
      </span>
    </div>
  </main>
</template>
