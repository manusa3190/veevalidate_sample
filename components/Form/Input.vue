<script setup lang="ts">
import { useField } from 'vee-validate';

const {name} = defineProps<{name:string}>();

const { handleChange, value, handleBlur, errorMessage, meta } = useField(() => name,undefined ); //第二引数にundefinedを渡さないと、無限再帰ループしてしまう

</script>

<template>
    <label class="form-control w-full max-w-xs">
        <div class="label">
        <span class="label-text">{{ name }}</span>
        <span v-if="meta.required" class="text-red-500">*</span>
        <span class="label-text-alt text-red-500">{{ errorMessage }}</span>
        </div>
        <input type="text" :value="value" @change="handleChange"  placeholder="Type here" class="input input-bordered w-full max-w-xs" />
    </label>
</template>