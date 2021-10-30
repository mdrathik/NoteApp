<template>
  <div class="col-span-8 mt-20 grid grid-cols-5 gap-y-6 gap-x-5">
    <Note :notes="notes" @deleteNote="deleteNote" @updateNote="updateNote" />
  </div>
</template>

<script>
import Note from './Note.vue';
export default {
  props:['notes'],
  components:{
  Note
  },
 data() {
    return {
        
    }
 },
    methods:{
       deleteNote(id){
        this.$emit('delete-Note',id);
       },
    updateNote(id){
     this.$emit('update-Note',id);
    }

    }

}
</script>

<style></style>
