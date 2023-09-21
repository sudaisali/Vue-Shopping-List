<template>
  <div class="container mt-5">
    <div class="card ">
      <div class="card-header d-flex justify-content-between align-items-center">
        <h1> {{ msg }} </h1>
        <div>
          <button v-if="editing" class="btn btn-secondary" @click="toEdit(false)"> Cancel</button>
        <button v-else class="btn btn-primary" @click="toEdit(true)"> ADD</button>
        </div>
        
      </div>
     
   
  </div>
</div>
<div :class="['container', 'mt-5', { 'd-lg-flex': editing }]">
    <div class="container">
      <div  v-if="editing" class="card justify-content-center ">
        <h1 class="card-header text-center">Add ITEMS</h1>
        <div class="container d-flex my-2" >
          <input type="text" v-model="addItem" placeholder="Add Item" class="form form-control w-75" >
          <button class="btn btn-primary p-0 w-25 mx-2"
          @click="saveItem"> Add Item</button>
         
        </div>
        <p class="bg-light mx-3">{{ count }}/100</p>
        <div class="form-check mx-3 mb-3">
        <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault" v-model="checkHighPriority">
        <label class="form-check-label" for="flexCheckDefault">
         High Priority
        </label>
</div>
       
      </div>
    </div>
    <div class="container">
      <div class="container" v-if="!list.length">
      <p class="fs-3">No Item in Container</p>
      </div>
      <div v-else class="  row justify-content-start">
       
      <div class="col-md-6 justify-content-center" v-for="item in reverseItem" :key="item.id" @click="purchItem(item)">
      <p class="bg-light fs-5 p-3 rounded" :class="{purchased: item.purchased, highlight:item.highPriority }">
        {{ item.label }}
      </p>
    
  </div>
    </div>
    </div>
  
  
    
  </div>
 
 
 
  
  
</template>

<script setup>
import { ref , computed } from 'vue';
const msg = ref('SHOPPING LIST')
const addItem = ref('')
const checkHighPriority = ref(false)
const editing = ref(false)
const list = ref([
  
  {id:1,label:'Sprite', purchased:true ,highPriority:true},
  {id:2,label:'Cocacola',purchased:false ,highPriority:true},
  {id:3,label:'Fanta',purchased:true ,highPriority:false},
  {id:4,label:'Shehzan',purchased:true ,highPriority:true},
  {id:5,label:'Red Bull',purchased:false ,highPriority:false},
  {id:6,label:'SLice',purchased:true ,highPriority:true},
  {id:7,label:'NextCola',purchased:false ,highPriority:true},
  {id:8,label:'DayFresh',purchased:true ,highPriority:false},
  {id:9,label:'Lemon malt',purchased:true ,highPriority:true},
  {id:10,label:'Meezan',purchased:false ,highPriority:true}

])

const count = computed(()=>{

  return addItem.value.length
  
})

const reverseItem = computed(()=>{
  return [...list.value].reverse()
})
const saveItem = ()=>{
  list.value.push(
    {
      id: list.value.length+1,
      label: addItem.value,
      highPriority: checkHighPriority.value

      
    }
  )
  addItem.value = ''
}

const toEdit = (e) =>{
  editing.value = e;
  addItem.value = ''
}

const purchItem = (item) =>{
 item.purchased = !item.purchased
}




</script>

<style scoped>
body{
  background-color: rgba(32, 32, 32, 0.295);
}
.card-header{
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  color: rgb(92, 90, 1);
}
.purchased{
 text-decoration: line-through;
}
.highlight{
  color: red;
}
@media(max-width: 768px){
  .card-header{
    text-align: center;
  }
}
</style>