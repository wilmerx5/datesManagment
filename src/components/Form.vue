<script setup>

import { reactive } from 'vue';
import Alert from './Alert.vue';



const alerta = reactive({
    type: '',
    message: '',
    active: false,

})



const emit=defineEmits(['update:pet', 'update:owner', 'update:email', 'update:date', 'update:symtomp','add-patient'])
const validate = (e) => {

    if (Object.values(props).includes('')) {

        alerta.type = "error"
        alerta.message = "there are empty fields"

        setTimeout(() => {
            alerta.message = ""
        }, 4000)

        return
    }
    emit('add-patient')
    alerta.type = "success"
    if(props.id){

        alerta.message = `patient card ${props.id} updated`
    }else{
        alerta.message = "patient card created"

    }

        setTimeout(() => {
            alerta.message = ""
        }, 4000)
}


const props = defineProps({
    pet: {
        type: String,
        required: true
    },
    owner: {
        type: String,
        required: true
    }, email: {
        type: String,
        required: true
    }, date: {
        type: String,
        required: true
    }, symtomp: {
        type: String,
        required: true
    },id:{
        type:[String,null],
        required:true
    
    }
})

</script>


<template>

    <div class="md:w-1/2">
        <h2 class="font-black text-3xl text-center"> Follow-up patiens</h2>
        <p class=" mt-5 text-2xl text-center mb-10">
            add patiens and <span class="text-indigo-600 font-b">manage them</span>
        </p>
        <Alert v-if="alerta.message" :alerta="alerta" />
        <form @submit.prevent="validate" class="bg-white shadow-md rounded-lg py-10 px-10 mb-10">
            <div class="mb-5">
                <label class=" block text-gray-700 uppercase font-bold" for="pet"> Name pet</label>
                <input :value="pet" @input="$emit('update:pet', $event.target.value)" type="text" placeholder="name pet"
                    id="pet"
                    class="mt-2 mb-2 outline-3 outline-gray-400 border-2 w-full p-2 placeholder-gray-400 rounded-md" />

                <label class=" block text-gray-700 uppercase font-bold" for="owner"> owner</label>
                <input @input="$emit('update:owner', $event.target.value)" type="text" placeholder="owner" id="owner"
                    :value="owner"
                    class="mt-2 mb-2 outline-3 outline-gray-400 border-2 w-full p-2 placeholder-gray-400 rounded-md" />

                <label class=" block text-gray-700 uppercase font-bold" for="email"> email</label>
                <input @input="$emit('update:email', $event.target.value)" type="email" placeholder="email" id="email"
                    :value="email"
                    class="mt-2 mb-2 outline-3 outline-gray-400 border-2 w-full p-2 placeholder-gray-400 rounded-md" />

                <label class=" block text-gray-700 uppercase font-bold" for="date"> date</label>
                <input @input="$emit('update:date', $event.target.value)" type="date" placeholder="email" id="date"
                    :value="date"
                    class="mt-2 mb-2 outline-3 outline-gray-400 border-2 w-full p-2 placeholder-gray-400 rounded-md" />

                <label class=" block text-gray-700 uppercase font-bold" for="Syntomps"> Syntomps</label>
                <textarea @input="$emit('update:symtomp', $event.target.value)" :value="symtomp" placeholder="Syntomps"
                    id="date"
                    class=" h-40 resize-none mt-2 mb-2 outline-3 outline-gray-400 border-2 w-full p-2 placeholder-gray-400 rounded-md" />


                <input type="submit" :value="id?'update':'submit'" class="bg-indigo-700 w-full p-3 text-white uppercase font-bold hover:bg-indigo-500
                    cursor-pointer transition-colors-2s">
            </div>

        </form>
    </div>
</template>