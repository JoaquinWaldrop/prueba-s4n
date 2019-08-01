<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8 md6>
      <ul>
        <nuxt-link
          v-for="project in projects"
          :key="project.fields.title"
          :to="`/projects/${project.fields.title}`"
        >
          <li>
            <h2>{{ project.fields.title }}</h2>
            <h3>{{ project.fields.year }}</h3>
            <h3>{{ project.fields.country.fields.title }}</h3>
          </li>
        </nuxt-link>
      </ul>
    </v-flex>
  </v-layout>
</template>

<script>
import client from '~/plugins/contentful'

export default {
  asyncData() {
    return client
      .getEntries({
        content_type: 'project',
        locale: 'en-US'
      })
      .then((entries) => {
        return { projects: entries.items }
      })
  }
}
</script>
