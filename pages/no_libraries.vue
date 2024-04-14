<script setup lang="ts">
definePageMeta({name:'1.ライブラリなし'})

const formData = reactive({
    名前:'',
    メールアドレス:''
})

const nameErrorMessage = computed(()=>{
    if(!formData.名前){
        return '名前を入力してください'
    }
})

const emailErrorMessage = computed(()=>{
    if(!formData.メールアドレス){
        return 'メールアドレスを入力してください'
    }
    if(!formData.メールアドレス.match(/^[a-zA-Z0-9_.+-]+@([a-zA-Z0-9][a-zA-Z0-9-]*[a-zA-Z0-9]*\.)+[a-zA-Z]{2,}$/)){
        return '正しいメールアドレスを入力してください'
    }
})

function onSubmit(){
    // ここでもバリデーションが必要
    alert(JSON.stringify(formData))
}

</script>

<template>

    <div class=" card card-bordered max-w-md border-2 m-4">
        <div class=" card-body">
            <div class=" card-title">ライブラリなし</div>

            <form @submit="onSubmit">
                <label class=" form-control max-w-sm">
                    <div class="label">
                        <span class=" label-text">名前</span>
                        <span class=" label-text-alt text-warning">{{ nameErrorMessage }}</span>
                    </div>
                    <input class="input input-sm input-bordered" v-model="formData.名前">
                </label>

                <label class=" form-control max-w-sm">
                    <div class="label">
                        <span class=" label-text">メールアドレス</span>
                        <span class=" label-text-alt text-warning">{{ emailErrorMessage }}</span>
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