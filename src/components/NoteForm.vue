<template>
    <div class="form">
        <textarea cols="30" rows="10" v-model="newText" @keyup.enter="saveNote"></textarea>
        <button @click="saveNote">save</button>
    </div>
</template>
<script>
export default{
    name:'NoteForm',
    emits:['save'],
    props:['noteText'],
    data(){
        return{
            newText:this.noteText,
            isChecked: false,
        }
    },
    watch: { 
        noteText(newVal) {
            this.newText = newVal;
        }
    },
    methods:{
        saveNote(){
            this.$emit('save', this.newText, this.isChecked);
            this.newText='';
        }
    }
}
</script>