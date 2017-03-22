<template>
  <div id="app">
    <toolbar :activeNote="activeNote"
             @addNote="addNote"
             @toggleFavorite="toggleFavorite"
             @deleteNote="deleteNote"
             @clearNote="clearNote"></toolbar>
    <notes-list :notes="notes" :activeNote="activeNote" @updateActiveNote="updateActiveNote"></notes-list>
    <editor :activeNote="activeNote" @edit="edit"></editor>
  </div>
</template>

<script>
    import Toolbar from './Toolbar.vue'
    import NotesList from './NotesList.vue'
    import Editor from './Editor.vue'

    export default {
        create() {
        },
        data() {
            return {
                notes: JSON.parse(localStorage.notes) || [],
                activeNote: {},
                count: 0
            }
        },
        components: {
            Toolbar,
            NotesList,
            Editor
        },
        methods: {
            addNote() {
                let newNote = {
                    text: 'New note ' + this.count++,
                    favorite: false,
                    index: this.notes.length
                }
                this.notes.push(newNote);
                this.activeNote = newNote;
                this.saveNote();
            },
            toggleFavorite() {
              var index = this.activeNote.index;
              this.notes[index].favorite = !this.notes[index].favorite;
              this.saveNote();
            },
            deleteNote() {
                this.notes.splice(this.activeNote.index, 1);
                for(var i = 0, len = this.notes.length; i < len; i++) {
                    this.notes[i].index = i;
                }

                if(this.notes.length) {
                    this.activeNote = this.notes[0];
                } else {
                    this.activeNote = {};
                }

                this.saveNote();
            },
            saveNote() {
                localStorage.notes = JSON.stringify(this.notes);
            },
            clearNote() {
                this.notes = [];
                this.activeNote = {};
                this.saveNote();
            },
            updateActiveNote(note) {
                this.activeNote = note;
                this.saveNote();
            },
            edit(activeNote, e) {
              this.activeNote.text = e.target.value;
                this.saveNote();
            }
        }
    }
</script>