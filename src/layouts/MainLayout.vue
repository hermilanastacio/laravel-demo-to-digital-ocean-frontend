<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title>
          Quasar App
        </q-toolbar-title>

        <div>Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      class="bg-grey-1"
    >
      <form class="q-py-xl q-px-md">
        <h6 class="q-ma-none">CREATE POST</h6>
        <q-input outlined dense v-model="title" label="Title" class="q-mb-md"/>
        <q-input outlined dense v-model="content" label="Content" class="q-mb-md"/>
        <q-input outlined dense v-model="author" label="Author" class="q-mb-md"/>
        <q-input outlined dense v-model="slug" label="Slug" class="q-mb-md"/>

        <q-file dense outlined label="Image" v-model="image" class="q-mb-md">
          <template v-slot:prepend>
            <q-icon name="attach_file" />
          </template>
        </q-file>

        <q-btn type="submit" color="primary" @click="handlePost" class="float-right" label="POST" />
      </form>
      <!-- <q-list>
        <q-item-label
          header
          class="text-grey-8"
        >
          Essential Links
        </q-item-label>

        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list> -->
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
/* eslint-disable */
import EssentialLink from 'components/EssentialLink.vue'

const linksList = [
  {
    title: 'Docs',
    caption: 'quasar.dev',
    icon: 'school',
    link: 'https://quasar.dev'
  },
  {
    title: 'Github',
    caption: 'github.com/quasarframework',
    icon: 'code',
    link: 'https://github.com/quasarframework'
  },
  {
    title: 'Discord Chat Channel',
    caption: 'chat.quasar.dev',
    icon: 'chat',
    link: 'https://chat.quasar.dev'
  },
  {
    title: 'Forum',
    caption: 'forum.quasar.dev',
    icon: 'record_voice_over',
    link: 'https://forum.quasar.dev'
  },
  {
    title: 'Twitter',
    caption: '@quasarframework',
    icon: 'rss_feed',
    link: 'https://twitter.quasar.dev'
  },
  {
    title: 'Facebook',
    caption: '@QuasarFramework',
    icon: 'public',
    link: 'https://facebook.quasar.dev'
  },
  {
    title: 'Quasar Awesome',
    caption: 'Community Quasar projects',
    icon: 'favorite',
    link: 'https://awesome.quasar.dev'
  }
]

import { defineComponent, ref } from 'vue'
import axios from 'axios'

export default defineComponent({
  name: 'MainLayout',

  components: {
    EssentialLink
  },
  data () {
    return {
      title: '',
      content: '',
      slug: '',
      author: '',
      image: null
    }
  },

  setup () {
    const leftDrawerOpen = ref(false)

    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  },
  methods: {
    handlePost(e) {
      e.preventDefault()

      var formData = new FormData();
      
      formData.append('title', this.title),
      formData.append('content', this.content),
      formData.append('slug', this.slug),
      formData.append('author', this.author),
      formData.append('image', this.image),

      axios.post('https://dev.hermilanastacio.info/api/post',
      formData, { 
        headers: {
          'Content-Type': 'application/x-www-form-urlencoded'
        }
      })

      // location.reload();
    }
  }
})
</script>
