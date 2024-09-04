
<script setup>
import { computed } from 'vue';


const props = defineProps({

    alerta:{
        type:Object,
        required:true
    }

})

const isError=computed(()=>{
   return props.alerta.type==="error"
})

</script>
<template>

<div
:class="[isError?'bg-red-500 ': 'bg-green-500']"
class="text-white text-center font-bold uppercase py-4"
>{{ alerta.message }}</div>
</template>