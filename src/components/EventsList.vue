<template>
  <div class="events container">
    <h2 class="subtitle is-3">
    Check out our upcoming events
    </h2>
    <div class="columns is-multiline">
      <div class="column is-one-quarter" v-for="event in events" v-bind:key="event.id" v-bind:event="event">
          <router-link :to="'/event/' + event.id">
            <EventCard :event="event" />
          </router-link>
      </div>
    </div>
  </div>
</template>
<script>
  import EventCard from '@/components/EventCard';
  import EventService from '@/services/EventService.js';
  export default {
    name: 'EventsList',
    components : {
      EventCard
    },
    data () {
      return {
        event: {},
        events: []
      }
    },
    created() {
      this.getEventsData();
    },
    methods: {
      async getEventsData() {
        EventService.getEvents().then(
          (event => {
            this.$set(this, "events", event);
          }).bind(this)
        )
      }
    }
  }
</script>
<style lang="scss" scoped>
  .events {
    margin-top: 100px;
    text-align: center;
  }
</style>
