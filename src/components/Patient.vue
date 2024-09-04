<script setup>


const props=defineProps({
    patient:{
        type:Array,
        required:true
    }
})

defineEmits(['update-card','delete-card'])
</script>
<template>
    <div  class="mx-5 my-10 bg-white shadow-md px-5 py-10 rounded-xl">
        <p class="font-bold mb-3 text-gray-700 uppercase">ID {{ patient.id }} 
            <span class="font-normal normal-case">
            
            </span>
        </p>

        <p class="font-bold mb-3 text-gray-700 uppercase">Pet: {{ props.patient.pet }}
            <span class="font-normal normal-case">
            
            </span>
        </p>

        <p class="font-bold mb-3 text-gray-700 uppercase">OWner: {{ props.patient.owner }}
            <span class="font-normal normal-case">
            
            </span>
        </p>

        <p class="font-bold mb-3 text-gray-700 uppercase">Email: {{ props.patient.email }}
            <span class="font-normal normal-case">
            
            </span>
        </p>

        <p class="font-bold mb-3 text-gray-700 uppercase">Date:{{ props.patient.date }}
            <span class="font-normal normal-case">
            
            </span>
        </p>

        <p class="font-bold mb-3 text-gray-700 uppercase">symtomp: {{ props.patient.symtomp }}
            <span class="font-normal normal-case">
            
            </span>
        </p>

        <div class="grid md:grid-cols-2  gap-5 mt-10 ">
            <button 
            @click="$emit('update-card',patient.id)"
                type="button"
                class="block w-full py-2 px-10 bg-indigo-600 hover:bg-indigo-700 text-white font-bold uppercase rounded-lg"
            >Editar</button>

            <button 
            @click="$emit('delete-card',patient.id)"
                type="button"
                class="block w-full py-2 px-10 bg-red-600 hover:bg-red-700 text-white font-bold uppercase rounded-lg"
            >Eliminar</button>
        </div>
    </div>

</template>