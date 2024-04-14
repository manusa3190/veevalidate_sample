<script setup lang="ts">
import { useField } from 'vee-validate';
import * as yup from 'yup'

definePageMeta({name:'3.useFieldを使用'})

const 名前field = useField('名前',yup.string().required('名前を入力してください'))
const メールアドレスfield = useField('メールアドレス',yup.string().email('正しいメールアドレスを入力してください').required('メールアドレスを入力してください'))

function onSubmit(){
    // ここは実装しづらい
}

</script>

<template>

    <div class=" card card-bordered max-w-md border-2 m-4">
        <div class=" card-body">
            <div class=" card-title">{{ $route.name }}</div>

            <form @submit="onSubmit">
                <label class=" form-control max-w-sm">
                    <div class="label">
                        <span class=" label-text">名前</span>
                        <span class=" label-text-alt text-warning" v-if="名前field.meta.dirty">{{ 名前field.errorMessage }}</span>
                    </div>
                    <input class="input input-sm input-bordered" :value="名前field.value.value" @input="名前field.setValue($event.target.value)">
                    <!-- これはダメ
                    <input class="input input-sm input-bordered" v-model="名前field.value"> -->
                </label>

                <label class=" form-control max-w-sm">
                    <div class="label">
                        <span class=" label-text">メールアドレス</span>
                        <span class=" label-text-alt text-warning" v-if="メールアドレスfield.meta.dirty">{{ メールアドレスfield.errorMessage }}</span>
                    </div>
                    <input type="email" class="input input-sm input-bordered" :value="メールアドレスfield.value.value" @input="メールアドレスfield.setValue($event.target.value)">
                </label>

                <div class=" card-actions">
                    <button class="btn btn-primary">送信</button>            
                </div>

            </form>
        </div>
    </div>

    <pre>名前value: {{ 名前field.value }}</pre>
    <pre>メールアドレスvalue: {{ メールアドレスfield.value }}</pre>

    <pre>名前error: {{ 名前field.errorMessage }}</pre>
    <pre>メールアドレスerror: {{ メールアドレスfield.errorMessage }}</pre>

</template>

<style scoped>
pre {
    @apply bg-slate-900 rounded-lg text-slate-400 m-3 p-3
}
</style>