<template>
  <div class="h-screen bg-white px-36 py-20">
    <Header
      @userNote="addNote"
      @userUpdateNote="userUpdateNote"
      :updateNoteData="updateNoteData"
    />
    <h1
      v-if="notes.length < 1"
      class="mt-20 p-10 text-6xl font-extrabold text-gray-300 text-center"
    >
      Please add your Note.
    </h1>
    <Grid
      v-else
      :notes="notes"
      @delete-Note="deleteNote"
      @update-Note="updateNote"
    />
  </div>
</template>
<script>
 import Header from './components/Header.vue'
 import Grid from './components/Grid.vue'

export default {

name: 'App',
watch: {
  notes: {
    handler() {
      localStorage.setItem('notes',JSON.stringify(this.notes))
    },
    deep: true
  }
},
mounted() {
  if (localStorage.getItem("notes")){
    this.notes = JSON.parse(localStorage.getItem("notes"))
  }
},
  components:{
    Header,
    Grid
  },
  data(){
    return{

              notes:[],
              updateNoteData:{},
    }
  },

  methods:{
    addNote(value){
      this.notes.unshift(value);
    },
    userUpdateNote(obj){
const updatedArray = this.notes.map(a => {
   if (a.id == obj['id']) {
      a.note = obj['note'];
   }
    this.updateNoteData={}

    
});
    },
    deleteNote(id){
      console.log(this.notes);
   const index = this.notes
        .map((x) => {
          return x.id
        })
        .indexOf(id)
      this.notes.splice(index, 1);
      this.updateNoteData ={}
    },
    updateNote(id){
      const updateObj= this.notes.findIndex(x => x.id === id);
      this.updateNoteData = this.notes[updateObj];
    }
  }
}
</script>

<style></style>
