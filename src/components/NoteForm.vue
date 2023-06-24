<template>
    <div class="mt-4">
      <h3>{{ isNewNote ? 'Create Note' : 'Edit Note' }}</h3>
      <form @submit.prevent="saveNote">
        <div class="mb-3 col-6">
          <label for="title" class="form-label">Title</label>
          <input type="text" id="title" class="form-control" v-model="currentNote.title" required>
        </div>
        <div class="mb-3 col-6">
          <label for="description" class="form-label">Description</label>
          <textarea id="description" class="form-control" v-model="currentNote.description" required></textarea>
        </div>
        <div class="mb-3">
          <div>{{ wordCount }} words</div>
          <div class="word-counter">{{ 1000 - wordCount }} words remaining</div>
        </div>
        <button type="submit" class="btn btn-primary">{{ isNewNote ? 'Create Note' : 'Save Note' }}</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    props: ['currentNote', 'isNewNote'],
    computed: {
      wordCount() {
        return this.currentNote.description.trim().split(/\s+/).length;
      }
    },
    methods: {
      saveNote() {
        this.$emit('save-note');
      }
    }
  };
  </script>
  