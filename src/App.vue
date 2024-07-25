<script setup>
import { uid } from 'uid';
import { onMounted, reactive, ref, watch } from 'vue';
import Form from './components/Form.vue';
import Header from './components/Header.vue';
import Patient from './components/Patient.vue';
const patients =ref([])

const patient = reactive({
  id:null,
    pet: "",
    owner: "",
    email: "",
    date: "",
    symtomp: ""


})
watch(patients,()=>{
    saveLocal()
  },{
    deep:true
  })

  const saveLocal=()=>{
    localStorage.setItem('patients',JSON.stringify(patients.value))
    console.log('savong')
  }
onMounted(()=>{
  const savedItem= localStorage.getItem('patients')
  if(savedItem){
    patients.value=JSON.parse(savedItem)
  }
})

const addPatient=()=>{
console.log(patients)
  if(patient.id){
    //update
    let index= patients.value.findIndex(i=>i.id===patient.id)

    console.log(index)
    patients.value[index]={...patient}
  }
  else{
    patients.value.push({...patient,id:uid()})


  }


  patient.pet=''
patient.owner=''
patient.email=''
patient.date=''
patient.symtomp=''
patient.id=null

  
}


const updateCard=(id)=>{
  const patientEdit = patients.value.filter((e)=>e.id===id)[0]
  Object.assign(patient,patientEdit)
  
}
const deleteCard=(id)=>{

   patients.value =  patients.value.filter(e=>e.id!==id)

}

</script>

<template>

<div class=" container mx-auto mt-20">
  <Header/>
  <div class="mt-12 md:flex">

    <Form
    v-model:pet="patient.pet"
    v-model:owner="patient.owner"
    v-model:email="patient.email"
    v-model:date="patient.date"
    v-model:symtomp="patient.symtomp"
    @add-patient="addPatient"
    :id="patient.id"


    ></Form>
    <div class="md:w-1/2 md:h-screen overflow-y-scroll">

      <h3 class="text-3xl text-center font-bold "> Admin your patients </h3>
      <p class="text-2xl text-center font-bold " >info<span class="text-indigo-500"> patients </span></p>
      

      <div v-if="patients.length>0" >
        <Patient
        v-for="patient in patients"
        :patient="patient"
        @update-card="updateCard"
        @delete-card ="deleteCard"
        />

      </div>
      <p v-else class="text-center py-5 text-2xl text-red-400">
        There are no patiens
      </p>

    </div>

  </div>
</div>
</template>

