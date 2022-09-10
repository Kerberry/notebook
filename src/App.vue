//блокнот
<template>
  <div class="container">
    <div class="notes-cont" v-if="notes.length>0">
      <SearchNote
        @searchNotes="searchNotes"
      />
      <Note v-for="note in notes" 
        :text="note.text"
        :isChecked="note.isChecked"
        :id="note.id"
        @checkNote="checkNote"
        @editNote="editNote"
        :key="note.id" 
      />
      <div class="btn-container">
        <button @click="delItem">delete</button>
        <button @click="delAll">delete all</button>
      </div>
    </div>
    <p v-else>You don`t have any notes</p>
    <NoteForm
      :noteText = "this.noteText"
      @save="save"
    />
  </div>
</template>

<script>
import Note from './components/Note.vue'
import NoteForm from './components/NoteForm.vue'
import SearchNote from './components/SearchNote.vue'
export default{
  name: 'App',
  components: {
    Note,
    NoteForm,
    SearchNote
  },
  data(){
    return{
      notes:[],
      noteText:'',
      id:null,
      visible:[],
    }
  },
  methods:{
    save(text, isChecked){
      if(this.noteText !== ''){
        this.notes[this.id].text = text
      }
      else{
        let id = this.notes.length;
        this.notes.push({id,text,isChecked});
      }
    },
    checkNote(id){
      if(!this.notes[id].isChecked){
        this.notes[id].isChecked = true;
      }
    },
    delItem(){
      this.notes = this.notes.filter((note)=> !note.isChecked)
    },
    delAll(){
      this.notes=[];
    },
    editNote(id){
      this.noteText= this.notes[id].text;
      this.id=id;
    },
    searchNotes(phrase, condition){

      if(phrase!=='' || condition==='Search'){
        this.visible = this.notes.filter((note)=> note.text.includes(phrase));
        [this.visible, this.notes] = [this.notes, this.visible];
      }
      else{
        this.notes = this.visible
      }

      

    }

  }
}
</script>

<style>
.container{
  display: flex;
  justify-content: space-around;
}
.notes-cont{
  display: flex;
  flex-direction: column;
}
.form{
  display: flex;
  flex-direction: column;
}
.btn-container{
  display: flex;
  justify-content: space-between;
}
button{
  margin: 10px;
  padding: 5px;
}
p{
  color:dimgray
}

</style>
