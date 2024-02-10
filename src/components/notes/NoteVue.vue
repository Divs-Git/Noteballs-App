<template>
  <div class="card mb-4">
    <div class="card-content">
      <div class="content">
        {{ note.content }}
        <div class="has-text-right has-text-grey-light mt-2">
          <small>{{ characterLength }} </small>
        </div>
      </div>
    </div>
    <footer class="card-footer">
      <a href="#" class="card-footer-item">Edit</a>
      <a href="#" class="card-footer-item" @click.prevent="handleDeleteNote">Delete</a>
    </footer>
  </div>
</template>

<script setup>
/*
imports
*/
import { computed } from 'vue'

/*
  props
*/
const props = defineProps({
  note: {
    type: Object,
    required: true
  }
})

/*
  emits
*/
const emits = defineEmits(['handleDeleteNote'])

/*
  character lengths
*/
const characterLength = computed(() => {
  const charLength = props.note.content.length
  const description = charLength === 1 ? 'character' : 'characters'
  return `${charLength} ${description}`
})

/*
  handle delete note
*/
const handleDeleteNote = () => {
  emits('handleDeleteNote', props.note.id)
}
</script>
