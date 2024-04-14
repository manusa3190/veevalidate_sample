<script setup lang="ts">
import { useForm } from 'vee-validate';
import * as yup from 'yup';

definePageMeta({name:'テスト'})

const prefs = [
  {prefName:'大阪府',regionName:'近畿地方'},
  {prefName:'京都府',regionName:'近畿地方'},
  {prefName:'兵庫県',regionName:'近畿地方'},
  {prefName:'東京都',regionName:'関東地方'},
  {prefName:'埼玉県',regionName:'関東地方'},
  {prefName:'千葉県',regionName:'関東地方'},
]

const { handleSubmit, values, errors } = useForm({
  initialValues:{
      名前:'',
      メールアドレス:'',
      性別:'男性',
      同居人:[]
  },
  validationSchema: yup.object().shape({
    名前: yup.string().required('名前は必須です'),
    メールアドレス:yup.string().required('メールアドレスは必須です').email('正しいメールアドレス形式で入力してください'),
    地方:yup.string().oneOf(['関東地方','近畿地方']).required('地方は必須です'),
    都道府県:yup.string().oneOf(['東京都','千葉県','埼玉県','大阪府','京都府','兵庫県']),
    性別: yup.string().oneOf(['男性','女性']),
    同居人:yup.array()
  }),
});

const onSubmit = handleSubmit(values => {
  alert(JSON.stringify(values, null, 2));
});
</script>

<template>
    <form @submit="onSubmit">
        <FormInput name="名前" />
        <FormInput name="メールアドレス" />
        <FormInput name="性別" />

        <FormSelect name="地方" :items="[...new Set(prefs.map(item=>item['regionName'])) ]"></FormSelect>

        <FormSelect name="都道府県" :items="prefs.filter(item=>item['regionName']===values['地方']).map(item=>item['prefName'])"></FormSelect>

        <FormArray name="同居人"></FormArray>

        <div class=" form-control">
            <button class="btn btn-primary">Submit</button>
        </div>      
    </form>

    <pre>{{ values }}</pre>
    <pre>{{ errors }}</pre>
</template>
  
