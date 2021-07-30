<template>
<form :class="classList" @submit.prevent="addCardToList">
 <input type="text" v-model="body"
        class="text-input" placeholder="Add new card"
        @focusin="startEditing" @focusout="finishEditing">
 <button class="add-button" type="submit" v-if="isEditing||bodyExists">
  add
 </button>
</form>
</template>

<script>
export default {
props:{
 listIndex:{
  type:Number,
  required: true,
 }
},
data: function(){
 return {
  body:'',
  isEditing: false,
 }
},
methods: {
 startEditing:function(){
  this.isEditing= true
 },
 finishEditing:function(){
  this.isEditing= false
 },
 addCardToList:function(){
  this.$store.dispatch('addCardToList',{body: this.body, listIndex: this.listIndex})
  this.body=''
 }
},
computed:{
 classList(){
  const classList = ['addcard']
  if(this.isEditing){
   classList.push('active')
  }
  if(this.bodyExists){
  classList.push('addable')
 }
  return classList
 },
 bodyExists(){
  return this.body.length > 0
 }
}
}
</script>