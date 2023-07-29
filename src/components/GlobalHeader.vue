
<script setup>
import { RouterLink } from "vue-router";
</script>


<template>
    <nav>
        <div class=" flex space-x-2 justify-between p-4 bg-slate-400">
            <div>
                Todo
            </div>

            <ul class=" flex space-x-2">
                <li>
                    <RouterLink to="/">Home</RouterLink>
                </li>
                <li>
                    <RouterLink to="/about">About</RouterLink>
                </li>
            </ul>
        </div>
    </nav>
  
</template>


<style lang="scss" scoped>

</style>