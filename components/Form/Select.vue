<script setup lang="ts">
import { useField } from 'vee-validate';

const props = defineProps<{name:string,items:string[]}>();

const { handleChange, value, handleBlur, errorMessage, meta,  } = useField(() => props.name, undefined ); 
</script>

<template>
<label>
    <div class="label">
        <span class=" label-text">{{ name }}</span>
        <span class=" text-red-500 label-text-alt">{{ errorMessage }}</span>
    </div>
    <select class="select select-bordered" :value="value" @change="handleChange">
        <option v-for="item of props.items" :key="item"
        :value="item">{{ item }}</option>
    </select>    
</label>

</template>