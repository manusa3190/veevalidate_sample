<script setup lang="ts">
import * as yup from 'yup'

definePageMeta({name:'2.yupのみ使用'})

const userSchema = yup.object().shape({
  名前: yup.string().required('名前を入力してください'),
  メールアドレス:yup.string().email('正しいメールアドレスを入力してください').required('メールアドレスを入力してください')
});

const formData = reactive({
    名前:'',
    メールアドレス:''
})

function onSubmit(){
    userSchema.validate(formData)
        .then(res=>{
            alert('OK')
        })
        .catch(err=>{
            alert(err)
        })
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
                        <!-- <span class=" label-text-alt text-warning">{{ nameErrorMessage }}</span> -->
                    </div>
                    <input class="input input-sm input-bordered" v-model="formData.名前">
                </label>

                <label class=" form-control max-w-sm">
                    <div class="label">
                        <span class=" label-text">メールアドレス</span>
                        <!-- <span class=" label-text-alt text-warning">{{ emailErrorMessage }}</span> -->
                    </div>
                    <input type="email" class="input input-sm input-bordered" v-model="formData.メールアドレス">
                </label>

                <div class=" card-actions">
                    <button class="btn btn-primary">送信</button>            
                </div>

            </form>
        </div>
    </div>

</template>