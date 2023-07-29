
<script setup>

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
    }

})



defineEmits([
    'toggle-complete', 
    'edit-todo', 
    'update-todo',
    'delete-todo'
])

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
                        <input 
                            name="updatedInput"
                            type="text" :value="todo.todo" class=" outline-none border-gray-800 border rounded-sm px-2"
                            v-if="todo.isEditing"
                            @input="$emit('update-todo', $event.target.value, index)"
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