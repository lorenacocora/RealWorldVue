<script setup>
import { ref, onMounted } from 'vue';
import EventService from "@/services/EventService.js"

const event = ref(null);

const props = defineProps({
  id: {
    required: true,
  }
})

onMounted(() => {
  EventService.getEvent(props.id)
    .then((response) => {
      event.value = response.data
    })
})
</script>


<template>
  <div v-if="event" class="event-details">
    <h1>{{ event.title }}</h1>
    <p>{{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
    <p>{{ event.description }}</p>
  </div>
</template>

<style>

.event-details {
  display: flex;
  flex-direction: column;
  align-items: center;
}

</style>