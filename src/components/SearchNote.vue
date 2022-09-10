<template>
    <div class="search">
        <input type="text" v-model="search" placeholder="Search here..."/>
        <input type="button" value="Search" @click="editSearch"/>
        
    </div>

</template>
<script>
    export default{
        data(){
            return{
                search:''
            }
        },
        methods:{
            editSearch(e){
                this.$emit('searchNotes',this.search, e.target.value);
                e.target.value = e.target.value==="Search"&&this.search!==''?"Cancel":"Search" ;
                this.search='';
            }
        }
    }
</script>
<style>
    .search>input{
        padding: 5px;
        margin-top:20px;
        margin-bottom: 10px;
    }
</style>