<template>
  <div id="app">
    <app-header></app-header>
    <div id="appContainer">
      <speech
        :addNote="addNote"
        :deleteNote="deleteNote"
        :removeAllNotes="removeAllNotes"
      />
      <note-item
        v-for="note in notes"
        :key="note.id"
        :noteItem="note"
      ></note-item>
    </div>
  </div>
</template>

<script>
import appHeader from "@/components/appHeader";
import noteItem from "@/components/noteItem";
import speech from "@/components/speech";

export default {
  components: {
    appHeader,
    noteItem,
    speech,
  },
  data() {
    return {
      // Load notes from localStorage on component initialization
      notes: JSON.parse(localStorage.getItem("notes")) || [],
      nnotes: [
        { id: 1, note: "note 1" },
        { id: 2, note: "note 2" },
        { id: 3, note: "note 3" },
        { id: 4, note: "note 4" },
      ],
    };
  },
  methods: {
    addNote(note) {
    const newNote = {
      id: this.notes.length + 1,
      note: note,
      timestamp: new Date().toLocaleString(),
    };
    this.notes.push(newNote);
    this.saveNotesToLocalStorage();
    },
  
    deleteNote(id) {
      this.notes.splice(
        this.notes.findIndex((n) => n.id == id),
        1
      );
      // Save notes to localStorage after deleting a note
      this.saveNotesToLocalStorage();
    },
    removeAllNotes() {
      this.notes = [];
      // Save notes to localStorage after removing all notes
      this.saveNotesToLocalStorage();
    },
    saveNotesToLocalStorage() {
      // Save notes to localStorage
      localStorage.setItem("notes", JSON.stringify(this.notes));
    },
  },
};
</script>
