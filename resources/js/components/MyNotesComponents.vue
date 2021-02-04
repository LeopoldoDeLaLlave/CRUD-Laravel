<template>
  <div class="row justify-content-center">
    <div class="col-md-8">
      <form-component @new="addNote"></form-component>

      <note-component
        v-for="(note, index) in notes"
        :key="note.id"
        :note="note"
        @update="updateNote(index, ...arguments)"
        @delete="deleteNote(index)"
      >
      </note-component>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      notes: [{ id: 1, description: "abc", created_at: "02/02/2021" }],
    };
  },
  methods: {
    addNote(note) {
      this.notes.push(note);
    },
    deleteNote(index){
        this.notes.splice(index, 1);
    },
    updateNote(index, note){
        
        this.notes[index]=note;
    }
  },
};
</script>

<style>
</style>