<script setup>
import CustomForm from "../components/CustomForm.vue";
import { uid } from "uid";
import { ref, watch, computed } from "vue";
import TodoItem from "../components/TodoItem.vue";
import gsap from 'gsap'

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
  todoList.value.unshift({
    id: uid(),
    todo,
    isCompleted: null,
    isEditing: null,
    invalid: null,
    errMsg: "",
  });
};

const toggleTodoComplete = (todoIndex) => {
  if(todoList.value[todoIndex].todo !== ""){
  todoList.value[todoIndex].isCompleted =
    !todoList.value[todoIndex].isCompleted;
  }
};

const toggleEditTodo = (todoIndex) => {

  if(todoList.value[todoIndex].todo !== ""){
    
  todoList.value[todoIndex].isEditing = !todoList.value[todoIndex].isEditing;
  }
};


const updateTodo = (todoValue, todoIndex) => {
  todoList.value[todoIndex].invalid = false;


  if(todoValue == ""){

    console.log(todoValue)
    todoList.value[todoIndex].invalid = true;
    todoList.value[todoIndex].errMsg = "Input required";
  }else{
    todoList.value[todoIndex].todo = todoValue;
  }
 
};

const deleteTodo = (todoIndex) => {
  if (window.confirm("Are You Sure?")) {
    todoList.value = todoList.value.filter((todo) => todo.id !== todoIndex);
  }
};

const beforeEnter=(el)=>{
  el.style.opacity=0;
  el.style.transform ='translateY(50px)';

}
const enter=(el, done)=>{
  gsap.to(el,{
    opacity:1,
    
    y:0,
    duration:.3,
    onComplete:done,
    delay:el.dataset.index * 0.2,
    ease:'bounce.out'
  })
}
const beforeLeave=(el)=>{
  el.style.opacity=0;
  el.style.transform ='translateY(50px)';

}
</script>

<template>
  <main class=" lg:mx-48 sm:mx-8 mx-0 px-4 ">
    <h1 class="pt-4 text-center text-2xl">Create Todo</h1>

    <CustomForm @create-todo="createTodo" />


    <div  v-if="todoList.length > 0" class="px-2 ">
 
      <!-- @before-enter="beforeEnter"
      @enter="enter"
      @before-leave="beforeLeave"
      @leave="leave" -->
    <transition-group 
      tag="ul" 
      name="list"
      appear 

      class=" relative">
      <TodoItem 
        v-for="(todo, index) in todoList"
        :data-index="index"
        :todo="todo"
        :index="index"
        :key="todo.id"

        @toggle-complete="toggleTodoComplete"
        @edit-todo="toggleEditTodo"
        @update-todo="updateTodo"
        @delete-todo="deleteTodo"
      />
    </transition-group>
    </div>
    <div  v-else class="flex justify-center text-center text-violet-800">
     Todo List Empty
    </div>

    <div class="flex justify-center text-center text-violet-800">
      <span v-if="todoCompleted && todoList.length > 0">
        Well Done! <br>Todo List Completed.
      </span>
    </div>
  </main>
</template>


<style scoped>
.list-enter-from{
  opacity: 0;
  transform: scale(0);
}
.list-enter-to{
  opacity: 1;
  transform: scale(1);
}
.list-enter-active{
  transition: all 0.5s ease;
}
.list-leave-from{
  opacity: 1;
  transform: scale(1);
}
.list-leave-to{
  opacity: 0;
  transform: scale(0.6);
}
.list-leave-active{
  transition: all 0.5s ease;
  position: absolute;
}

.list-move{
  transition: all 0.5s ease;
}


/* 
.todo-switch-enter-from,
.todo-switch-leave-to{
  opacity: 0;
  transform: translateY(20px);
}
.todo-switch-enter-active,
.todo-witch-leave-active{
  transition: all 0.5s ease;
} */
</style>
