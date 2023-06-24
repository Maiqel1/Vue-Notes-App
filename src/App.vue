<template>
  <div id="app" class="container mt-5">
    <h1>Notes App</h1>
    <NoteList :notes="notes" @edit-note="editNote" @delete-note="deleteNote" />
    <NoteForm :current-note="currentNote" :is-new-note="isNewNote" @save-note="saveNote" />
  </div>
</template>

<script>
import NoteList from './components/NoteList.vue';
import NoteForm from './components/NoteForm.vue';

export default {
  components: {
    NoteList,
    NoteForm,
  },
  data() {
    return {
      notes: [],
      currentNote: {
        title: '',
        description: ''
      },
      isNewNote: true
    };
  },
  mounted() {
    const savedNotes = localStorage.getItem('notes');
    if (savedNotes) {
      this.notes = JSON.parse(savedNotes);
    }
  },
  methods: {
    saveNote() {
      if (this.isNewNote) {
        this.notes.unshift(this.currentNote);
      }
      localStorage.setItem('notes', JSON.stringify(this.notes));
      this.currentNote = {
        title: '',
        description: ''
      };
      this.isNewNote = true;
    },
    editNote(note) {
      this.currentNote = { ...note };
      this.isNewNote = false;
    },
    deleteNote(note) {
      if (confirm('Are you sure you want to delete this note?')) {
        const index = this.notes.indexOf(note);
        if (index !== -1) {
          this.notes.splice(index, 1);
        }
        localStorage.setItem('notes', JSON.stringify(this.notes));
      }
    }
  }
};
</script>
