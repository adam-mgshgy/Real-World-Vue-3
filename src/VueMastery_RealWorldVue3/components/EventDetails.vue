<script setup lang="ts">
  import IEvent from "../types/IEvent";
  import EventService from "../services/EventService";
  import { ref } from "vue";
  import { useRoute } from "vue-router";

  const route = useRoute();
  const id = route.params.id;
  const event = ref<IEvent>();
  EventService.getEvent(id)
    .then((response) => {
      event.value = response.data;
    })
    .catch((error) => {
      console.log(error);
    });
  // export default {
  //   props: ["id"],
  //   data() {
  //     return {
  //       event: null,
  //     };
  //   },
  //   created() {
  //     EventService.getEvent(this.id)
  //       .then((response) => {
  //         this.event = response.data;
  //       })
  //       .catch((error) => {
  //         console.log(error);
  //       });
  //   },
  // };
</script>
<template>
  <div v-if="event">
    <h1>{{ event.title }}</h1>
    <p>{{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
    <p>{{ event.description }}</p>
  </div>
</template>
