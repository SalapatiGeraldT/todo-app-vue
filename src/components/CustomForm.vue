<script setup>
import { reactive, defineEmits } from 'vue';
import CustomButton from "../components/CustomButton.vue";
import CustomInput from './CustomInput.vue';

const todoState = reactive({
    todo: "",
  invalid: null,
  errMsg: "",
   
});


const emit = defineEmits([
    "create-todo"
]);

const createTodo = () => {

  todoState.invalid = false;
    if (todoState.todo !== "") {

        emit('create-todo', todoState.todo);
        todoState.todo = "";
    }else{
      todoState.invalid = true;
 
      todoState.errMsg = "Input required";

    }

};



const validateInput = () => {
  todoState.invalid = false;
  if (todoState.todo === "") {
    todoState.invalid = true;
 
    todoState.errMsg = "Input required";
  } else {
  }
};
// const inputValue = (input) => {
//     todoState.todo = input;
// };

</script>


<template>
    <div class=" flex flex-col py-4 space-y-2">
  
        <form @submit.prevent="createTodo(todoState)"
        class=" flex space-x-2"
        >

          <label for="todoInput" class=" text-center"></label>

        <CustomInput 
        class="w-full"
        required
        name="todoInput"
        placeholder="Enter your todo list"
        type="text"
          @input="[
            validateInput()
          ]
            
          "
            :value="todoState.todo"
            @input-value="(input) => { todoState.todo = input }"
        :class="{ 'border-red-700 border-4': todoState.invalid }"
        :index="0"
        />

   
    
        <CustomButton  type="submit" name="Button">
            Create
        </CustomButton>
      </form>
      <transition name="error-alert">
          <p v-show="todoState.invalid" class="text-red-700 text-center">
            {{ todoState.errMsg }}
          </p>
        </transition>
    </div>
</template>

<!-- :disabled="todoState.invalid" -->

<style  scoped>
/* .error-alert-enter-from{
  opacity: 0;
  transform: translateY(-60px);
}
.error-alert-enter-to{
  opacity: 1;
  transform: translateY(0);
} */
.error-alert-enter-active{
  /* transition: all 0.3s ease; */
  animation: wobble 0.5s ease;
}
.error-alert-leave-from{
  opacity: 1;
  transform: translateY(0);
}
.error-alert-leave-to{


  opacity: 0;
  transform: translateY(-60px);
}
.error-alert-leave-active{
  transition: all 0.3s ease-in;
}

@keyframes wobble {

  0%{transform: translateY(-60px); opacity: 0;}
  50%{transform: translateY(0px); opacity:1;}
  60%{transform: translateX(8px);}
  70%{transform: translateX(-8px);}
  80%{transform: translateX(4px);}
  90%{transform: translateX(-4px);}
  100%{transform: translateX(0px);}

}

</style>