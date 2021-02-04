<template>
  <div class="card">
    <div class="card-header">Publicado en: {{ note.created_at }} - Actualizado en: {{ note.updated_at }}</div>

    <div class="card-body">
      <input
        v-if="editMode"
        type="text"
        class="form-control"
        v-model="note.description"
      />

      <p v-else>{{ note.description }}</p>
    </div>

    <div class="card-footer">
      <button v-if="editMode" class="btn btn-succes" @click="onClickUpdate()">
        Guardar Cambios
      </button>
      <button v-else class="btn btn-default" @click="onClickEdit()">
        Editar
      </button>
      <button class="btn btn-danger" @click="onClickDelete()">Eliminar</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["note"],
  data() {
    return {
      editMode: false,
    };
  },
  methods: {
    onClickDelete() {
      axios
        .delete(`/EjerciciosLaravel/NotesLaravel/public/notes/${this.note.id}`)
        .then(() => {
          this.$emit("delete");
        });
      
    },
    onClickEdit() {
      this.editMode = true;
    },
    onClickUpdate() {
      

      const params = {
        description: this.note.description,
      };
      axios
        .put(`/EjerciciosLaravel/NotesLaravel/public/notes/${this.note.id}`, params)
        .then((response) => {
          this.editMode = false;
          const rnote = response;
          this.$emit("update", rnote);
        });
      
    },
  },
};
</script>
