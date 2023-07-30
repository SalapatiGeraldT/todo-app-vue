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
        <label for="todoInput" class=" text-center"></label>
  
        <form @submit.prevent="createTodo(todoState)">


        <CustomInput 
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
        <p v-show="todoState.invalid" class="text-red-700 text-center">
    {{ todoState.errMsg }}
  </p>
        <CustomButton  type="submit" name="Button">
            Create
        </CustomButton>
      </form>
       
    </div>
</template>

<!-- :disabled="todoState.invalid" -->

<style lang="scss" scoped></style>