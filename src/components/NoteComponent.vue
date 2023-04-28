<template>
  <div class="note-container">
    <h3>My Notes</h3>
    <div class="notes">
      <div class="note" v-for="(note, index) in notes" :key="index">
        <div class="note-text">{{ note.text }}</div>
        <button @click="deleteNote(index)">Delete</button>
      </div>
    </div>
    <div class="new-note">
      <textarea v-model="newNote" placeholder="Write a new note..."></textarea>
      <button @click="addNote">Add Note</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newNote: "",
      notes: [],
    };
  },
  methods: {
    addNote() {
      if (this.newNote.trim()) {
        this.notes.push({ text: this.newNote.trim() });
        this.newNote = "";
      }
    },
    deleteNote(index) {
      this.notes.splice(index, 1);
    },
  },
};
</script>

<style scoped>
.note-container {
  max-width: 600px;
  margin: 0 auto;
}

.notes {
  margin-bottom: 20px;
}

.note {
  background-color: #f5f5f5;
  border: 1px solid #e0e0e0;
  border-radius: 4px;
  padding: 15px;
  margin-bottom: 10px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.note-text {
  margin-right: 10px;
  font-size: 20px;
}

.new-note textarea {
  width: 100%;
  min-height: 100px;
  resize: vertical;
  margin-bottom: 10px;
  padding: 10px;
  border: 1px solid #e0e0e0;
  border-radius: 4px;
  font-size: 20px;
}

button {
  background-color: #42b983;
  color: #fff;
  padding: 8px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #35a56d;
}
</style>
