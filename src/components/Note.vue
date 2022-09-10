<template>
  <div class="notes-item">
    <input @click="$emit('checkNote', id)" type="checkbox" />
    <div @click="$emit('editNote', id)">{{text.length > 20?text.slice(0, 20) + '...':text}}</div>      
  </div>
</template>

<script>
  
export default {
  name: 'NoteN',
  
  props: {
    id:Number,
    text: String,
    isChecked:Boolean
  },
  
}
</script>

<style>
  .notes-item{
    display: flex;
    border: 1px solid gray;
    margin-top: 10px;
    padding: 10px;
  }
</style>
