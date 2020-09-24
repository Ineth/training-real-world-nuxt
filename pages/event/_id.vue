<template>
  <div>
    <h1>{{ event.title }}</h1>
  </div>
</template>

<script>
import eventApi from '~/apis/event.api'

export default {
  async asyncData({ $axios, error, params }) {
    try {
      const { data } = await eventApi.getEvent(params.id)
      return {
        event: data,
      }
    } catch (e) {
      error({
        statusCode: 503,
        message: 'unable to fetch events at this time.',
      })
    }
  },
  head() {
    return {
      title: 'Event #' + this.event.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Info about event #' + this.event.title,
        },
      ],
    }
  },
  computed: {
    id() {
      return this.$route.params.id
    },
  },
}
</script>

<style lang="scss" scoped></style>
