<template>
  <div class="notes">
    <div class="card has-background-info-dark p-4 mb-5">
      <div class="field">
        <div class="control">
          <textarea
            v-model="newNote"
            class="textarea"
            placeholder="Add a new note"
            ref="newNotesRef"
          ></textarea>
        </div>
      </div>

      <div class="field is-grouped is-grouped-right">
        <div class="control">
          <button class="button is-link has-background-info" :disabled="!newNote" @click="addNote">
            Add new note
          </button>
        </div>
      </div>
    </div>

    <NoteVue v-for="note in notes" :key="note.id" :note="note" @handle-delete-note="deleteNote" />
  </div>
</template>

<script setup>
/*
  imports
*/
import { ref } from 'vue'
import NoteVue from '@/components/notes/NoteVue.vue'

/*
  notes
*/
const newNote = ref('')
const newNotesRef = ref(null)

const notes = ref([
  {
    id: 'id1',
    content:
      'Lorem ipsum dolor sit amet consectetur adipisicing elit. Cupiditate sunt soluta, eaque quasi veniam saepe natus aliquam explicabo numquam repudiandae laboriosam ea inventorecorporis voluptatibus eveniet mollitia expedita dicta vitae.'
  },
  {
    id: 'id2',
    content: 'This one is a shorter note.'
  }
])

/*
  add note
*/
const addNote = () => {
  let time = new Date().getTime(),
    id = time.toString()

  let note = {
    id,
    content: newNote.value
  }

  notes.value.unshift(note)
  newNote.value = ''
  newNotesRef.value.focus()
}

/*
  delete note
*/
const deleteNote = (deleteNoteId) => {
  notes.value = notes.value.filter((note) => note.id !== deleteNoteId)
}
</script>
