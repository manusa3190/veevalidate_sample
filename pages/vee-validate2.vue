<script setup lang="ts">
import { useForm } from 'vee-validate';
import * as yup from 'yup'

definePageMeta({name:'4.useFormを使用'})

const {handleSubmit,values, errors, setValues} = useForm({
    validationSchema:{
        名前:yup.string().required('名前を入力してください'),
        メールアドレス:yup.string().email('正しいメールアドレスを入力してください').required('メールアドレスを入力してください')
    }
})

const onSubmit = handleSubmit(values=>{
    alert(JSON.stringify(values))
})

</script>

<template>

    <div class=" card card-bordered max-w-md border-2 m-4">
        <div class=" card-body">
            <div class=" card-title">{{ $route.name }}</div>

            <form @submit="onSubmit">
                <label class=" form-control max-w-sm">
                    <div class="label">
                        <span class=" label-text">名前</span>
                        <span class=" label-text-alt text-warning">{{ errors.名前 }}</span>
                    </div>
                    <input class="input input-sm input-bordered" :value="values.名前" @input="setValues({名前:$event.target.value})">
                </label>

                <label class=" form-control max-w-sm">
                    <div class="label">
                        <span class=" label-text">メールアドレス</span>
                        <span class=" label-text-alt text-warning">{{ errors.メールアドレス }}</span>
                    </div>
                    <input type="email" class="input input-sm input-bordered" :value="values.メールアドレス" @input="setValues({メールアドレス:$event.target.value})">
                </label>

                <div class=" card-actions">
                    <button class="btn btn-primary">送信</button>            
                </div>

            </form>
        </div>
    </div>

    <pre>values: {{ values }}</pre>

    <pre>errors: {{ errors }}</pre>

</template>

<style scoped>
pre {
    @apply bg-slate-900 rounded-lg text-slate-400 m-3 p-3
}
</style>