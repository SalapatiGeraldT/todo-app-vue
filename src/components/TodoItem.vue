
<script setup>
import CustomInput from './CustomInput.vue';
import { reactive, defineEmits } from 'vue';

const props = defineProps({
    todo:{
        type: Object,
        required: true,
        // default(){
        //     return
        // }
    },
    index:{
        type: Number,
        required: true,
    },
  

})

// const todoState = reactive({

//   invalid: null,
//   errMsg: "",
   
// });

defineEmits([
    'toggle-complete', 
    'edit-todo', 
    'update-todo',
    'delete-todo'
])
// const validateInput = (input, index) => {
//  todoList.value[index].invalid = false;
//   if (input === "") {
//    todoList.value[index].invalid = true;
    
//    todoList.value[index].errMsg = "Input required";
//   } else {
//   }
// };

// const inputValue = (input, index) => {
//     todo.value[index].todo = input;
// };

// const inputValue = (input, index) => {
//   const updatedTodo = { ...props.todo }; // Create a shallow copy of 'props.todo'
//   updatedTodo[index].todo = input; // Update the specific todo item with the new input
// //   emit('update-todo', updatedTodo); // Emit the 'update-todo' event with the updated todo as the payload
// };

</script>



<template>
        <li class="group">
            <div class=" flex flex-wrap justify-between  border-b-2">
                <div class=" flex content-center space-x-2 p-2">
                    <div>
                        <label for="todoDoneToggle"></label>
                        <input name="todoDoneToggle"
                            placeholder="todoDoneToggle"
                            title="todoDoneToggle"
                            class=" bg-blue-500 "
                            :checked="todo.isCompleted"
                            type="checkbox"
                            @input="$emit('toggle-complete', index)"
                        > 
                        
                    </div>
                    <div>
                        <label for="updatedInput"></label>
                        <!-- <input 
                            name="updatedInput"
                            type="text" 
                            :value="todo.todo" class=" outline-none border-gray-800 border rounded-sm px-2"
                         
                            @input="$emit('update-todo', $event.target.value, index)"
                            /> -->
                            
                            <CustomInput 
                            name="updatedInput"
                            type="text" 
                            :value="todo.todo"
                            :index="index"
                            @input="
                                [  
                                
                                    $emit('update-todo', $event.target.value, index)
                                ]

                                "
                            @input-value="(input) => { todo.todo = input }"
                            v-if="todo.isEditing"
                            :class="{ 'border-red-700 border-4': todo.invalid }"
                            />
                       
                        <span 
                        v-else
                        class="
                        decoration-slate-700
                        decoration-4 cursor-pointer
                        "
                        :class="{ ' line-through': todo.isCompleted }"
                        @click="$emit('toggle-complete', index)"
                        >
                            {{ todo.todo }}
                        </span>
                        <p v-show="todo.invalid" class="text-red-700 text-center">
                                {{ todo.errMsg }}
                            </p>
                    </div>
                </div>
                <div class="group-hover:flex hidden space-x-2 items-center">
                    <div v-if="todo.isEditing"
                    class=" cursor-pointer"
                    @click="$emit('edit-todo', index)"
                    >
                        Save
                    </div>
                    <div v-else
                    class=" cursor-pointer"
                    @click="$emit('edit-todo', index)"
                    >
                        Edit
                    </div>
                    <div
                    @click="$emit('delete-todo', todo.id)"
                    class=" cursor-pointer"
                    >
                        Delete
                    </div>
                </div>
            </div>

        </li>

</template>



<style lang="scss" scoped></style>