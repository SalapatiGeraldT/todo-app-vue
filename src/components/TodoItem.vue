
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
        <li class="group ease-in duration-600
            hover:bg-gradient-to-r from-blue-400 via-transparent to-pink-400">
            
            <div class=" flex flex-wrap justify-between  border-b-2 p-2">
                <div class=" flex content-center items-center space-x-2 ">
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
                        <transition name="error-alert">
                        <p v-show="todo.invalid" class="text-red-700 text-center">
                                {{ todo.errMsg }}
                            </p>
                        </transition>
                    </div>
                </div>
                <div class="group-hover:flex hidden space-x-2 items-center
                  justify-center  text-white
                ">
                    <div v-if="todo.isEditing"
                    class=" bg-slate-900  p-1 border-1 border-slate-500 border rounded-md cursor-pointer"
                    @click="$emit('edit-todo', index)"
                    >
                        Save
                    </div>
                    <div v-else
                    class=" bg-slate-900  p-1 border-1 border-slate-500 border rounded-md cursor-pointer"
                    @click="$emit('edit-todo', index)"
                    >
                        Edit
                    </div>
                    <div
                    @click="$emit('delete-todo', todo.id)"
                    class=" bg-slate-900  p-1 border-1 border-slate-500 border rounded-md cursor-pointer"
                    >
                        Delete
                    </div>
                </div>
            </div>

        </li>

</template>



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