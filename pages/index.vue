<template>
  <div>
    <h1>Events</h1>
    <EventCard
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>

<script>
import EventCard from '@/components/EventCard.vue'
export default {
  components: {
    EventCard,
  },
  head() {
    return {
      title: 'Event Listing',
    }
  },
  asyncData({ $axios, error }) {
    console.log('error: ', error)
    return $axios
      .get('http://localhost:3001/events')
      .then((response) => {
        return {
          events: response.data,
        }
      })
      .catch((e) => {
        error({
          statusCode: 503,
          message: 'unable to fetch events at this time.',
        })
      })
  },
}
</script>
