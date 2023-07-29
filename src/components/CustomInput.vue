<script setup>
import { reactive, defineEmits } from 'vue';
import CustomButton from "../components/CustomButton.vue";

const todoState = reactive({
    todo: "",
    invalid: null,
    errMsg: ""
});


const emit = defineEmits([
    "create-todo"
]);

const createTodo = () => {


    todoState.invalid = false;
    if (todoState.todo !== "") {

        emit('create-todo', todoState.todo);
        todoState.todo = "";
    } else {
        todoState.invalid = true;

        todoState.errMsg = "Input required";
    }

};
const validateInput = () => {


    todoState.invalid = false;
    if (todoState.todo === "") {
        todoState.invalid = true;

        todoState.errMsg = "Input required";

    }

};

</script>


<template>
    <div class=" flex flex-col py-4 space-y-2">
        <!-- {{ todo }} -->
        <label for="todoInput" class=" text-center"></label>
        <input name="todoInput"
            placeholder="Enter your todo list"
            :class="{ 'border-red-700 border-4': todoState.invalid }" 
            class=" p-1 outline-none rounded-sm hover:bg-green-200 focus:ring-2 
            border-green-800 border
            focus:ring-green-900" type="text" @input="validateInput()" v-model="todoState.todo" />

        <!-- <button :class="{ ' bg-slate-700 hover:bg-slate-700 hover:text-slate-50': todoState.invalid }" class="bg-green-900
        hover:bg-green-200 hover:text-black text-white py-1 px-6 rounded-sm
            
            " type="submit" :disabled="todoState.invalid" @click="createTodo()">
            Submit
        </button> -->

        <CustomButton @click="createTodo()">
            Create
        </CustomButton>
        <p v-show="todoState.invalid" class=" text-red-700 text-center">{{ todoState.errMsg }}</p>
    </div>
</template>

<!-- :disabled="todoState.invalid" -->

<style lang="scss" scoped></style>