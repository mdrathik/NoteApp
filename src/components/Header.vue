<template>
  <nav class="flex justify-items-center gap-x-20">
    <h1 class="text-7xl font-extrabold">Notes</h1>
    <div class="w-3/5">
      <label class="block text-left">
        <textarea
          v-if="isEmpty==false"
          v-on:keyup.enter="updateNote"
          v-model="editNote"
          class="form-textarea mt-1 block w-full border-4 border-gray-00 rounded-md p-2 shadow-md"
          required
          rows="3"
          placeholder="Hit Enter"
        >
        </textarea>
        <textarea
          v-else
          v-on:keyup.enter="addNote"
          v-model="userNote"
          class="form-textarea mt-1 block w-full border-4 border-gray-00 rounded-md p-2 shadow-md"
          rows="3"
          placeholder="Add Your Note & Hit Enter"
        >
        </textarea>
      </label>
      {{getEditNote}}
      Edit {{isEmpty}}
    </div>
  </nav>
</template>

<script>
export default {
  props:{
    updateNoteData:{
      note:String,
      required: true
    }
  },
  computed:{
    getEditNote(){
      if(this.updateNoteData['note']!=null){
     return this.editNote=this.updateNoteData['note'] }
    },
   isEmpty() {
  const data=this.editNote;
   if(typeof(data) === 'object') {
        if(JSON.stringify(data) === '{}' || JSON.stringify(data) === '[]') {
            return true;
        } else if(!data) {
            return true;
        }
        return false;
    } else if(typeof(data) === 'string') {
        if(!data.trim()){
            return true;
        }
        return false;
    } else if(typeof(data) === 'undefined') {
        return true;
    } else {
        return false;
    }
   }
  },
  data(){
    return {
      editNote : '',
      editNoteCount : 0,
      userNote: '',
      color:["bg-red-100","bg-yellow-100","bg-green-100","bg-indigo-100","bg-purple-100","bg-pink-100","bg-blue-100"],
    }
  },
  methods:{

    addNote() {
        const str = (this.userNote).replace(/\s/g,'');
        if(str.length>1){
        const today = new Date();
        const date = today.getFullYear()+'-'+(today.getMonth()+1)+'-'+today.getDate();
        const time = today.getHours() + ":" + today.getMinutes();
         const obj = {
        id : new Date().valueOf(),
        note: this.userNote,
        createdDate : `${time}, ${date}`,
        color: this.color[Math.floor(Math.random()*this.color.length)]
      }

            this.$emit('userNote',obj)
            this.userNote='';
        }
    },
updateNote(){
        const str = (this.editNote).replace(/\s/g,'');
        if(str.length>1){
          const today = new Date();
        const date = today.getFullYear()+'-'+(today.getMonth()+1)+'-'+today.getDate();
        const time = today.getHours() + ":" + today.getMinutes();
         const obj = {
        id : this.updateNoteData['id'],
        note: this.editNote,
        createdDate : `${time}, ${date}`,
        color: this.updateNoteData['color']
        }
            this.$emit('userUpdateNote',obj)
            this.editNote='';
        }
        else
        {
          console.log("Empty not allowed");
        }
}
    // updateNote(){
      //   const str = (this.updateNoteData['note']).replace(/\s/g,'');
      //   if(str.length>1){
      //   const today = new Date();
      //   const date = today.getFullYear()+'-'+(today.getMonth()+1)+'-'+today.getDate();
      //   const time = today.getHours() + ":" + today.getMinutes();
      //    const obj = {
      //   id : this.updateNoteData['id'],
      //   note: this.updateNoteData['note'],
      //   createdDate : `${time}, ${date}`,
      //   color: this.updateNoteData['color']
      // }
      //       this.$emit('UpdateUserNote',obj);

    //     }

    // }
  }
}
</script>

<style></style>
