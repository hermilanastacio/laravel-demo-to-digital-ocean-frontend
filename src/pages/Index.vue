<template>
  <q-page class="flex column">
    <q-card
      class="my-card text-white q-ma-xs"
      style="background: radial-gradient(circle, #35a2ff 0%, #014a88 100%)"
      v-for="post in posts" :key="post.id"
    >
      <q-card-section>
        <div class="text-h6">{{ post.title }}</div>
        <div class="text-subtitle2">by {{ post.author }} on {{ formatDate(post.created_at) }}</div>
        <span></span>
      </q-card-section>

      <q-card-section class="q-pt-none">
        {{ post.content }}
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script>
/* eslint-disable */
import { defineComponent } from 'vue'
import moment from 'moment'
import axios from 'axios'

export default defineComponent({
  name: 'PageIndex',
  data () {
    return {
      posts: []
    }
  },
  created() {
    axios.get('https://dev.hermilanastacio.info/api/post')
      .then(res => { 
        console.log(res.data)
        this.posts = res.data 
      })
  },
  methods: {
    formatDate(date) {
      return moment(date).format('ll')
    }
  }
})

</script>
