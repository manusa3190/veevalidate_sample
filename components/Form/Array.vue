<script setup lang="ts">
import { useFieldArray } from 'vee-validate';

const {name} = defineProps<{name:string}>();

const { remove, push, update, fields } = useFieldArray(() => name ); 

function handleUpdate(i,key,value){
    const rowItem = fields.value[i].value
    rowItem[key] = value
    update(i,rowItem)
}

</script>

<template>
    <table class="table table-sm border">
        <caption class=" text-start card-title">{{ name }}</caption>
        <tbody>
            <tr v-for="(f,i) of fields">
                <td>
                    <select class="select select-sm select-bordered"
                     :value="f.value['関係']" @change="handleUpdate(i,'関係',$event.target.value)">
                        <option v-for="o of ['父','母','きょうだい']" :value="o">{{ o }}</option>
                    </select>
                </td>
                <td>
                    <input class=" input input-sm input-bordered"
                     type="text"
                     :value="f.value['名前']" @input="handleUpdate(i,'名前',$event.target.value)">
                </td>
                <td @click="remove(i)">削除</td>
            </tr>
        </tbody>
        <button class="btn btn-primary" @click="push({関係:'',名前:''})">追加</button>
    </table>
</template>