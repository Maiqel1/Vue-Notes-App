<template>
    <div class="mt-4">
      <h3>Notes</h3>
      <ul class="list-group">
        <li v-for="note in notes" :key="note.id" class="list-group-item">
          <h5>{{ note.title }}</h5>
          <p>{{ note.description }}</p>
          <button class="btn btn-danger btn-sm float-end" @click="deleteNote(note)">Delete</button>
          <button class="btn btn-primary btn-sm float-end me-2" @click="editNote(note)">Edit</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    props: ['notes'],
    methods: {
      editNote(note) {
        this.$emit('edit-note', note);
      },
      deleteNote(note) {
        this.$emit('delete-note', note);
      }
    }
  };
  </script>