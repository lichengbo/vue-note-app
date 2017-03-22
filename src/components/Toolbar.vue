<template>
    <div id="toolbar">
        <i @click="addNote" title="add note" class="glyphicon glyphicon-plus"></i>
        <i @click="toggleFavorite" title="toggle favorite" class="glyphicon glyphicon-star" :class="{starred: activeNote.favorite}"></i>
        <i @click="deleteNote" title="delete note" class="glyphicon glyphicon-remove-circle"></i>
        <i @click="clearNote" title="clear all note" class="glyphicon glyphicon-remove"></i>
    </div>
</template>

<script>

    export default {
        props: {
            activeNote: Object
        },
        methods: {
            addNote() {
                this.$emit("addNote");
            },
            toggleFavorite() {
                this.$emit("toggleFavorite");
            },
            deleteNote() {
                this.$emit("deleteNote");
            },
            clearNote() {
                this.$emit("clearNote");
            }
        }
    }
</script>
