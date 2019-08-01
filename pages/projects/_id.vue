<template>
  <div>
    <h1>{{ project.fields.title }}</h1>
  </div>
</template>

<script>
import client from '~/plugins/contentful'

export default {
  asyncData(context) {
    return client
      .getEntries({
        content_type: 'project',
        'fields.title': context.params.id
      })
      .then((entries) => {
        return { project: entries.items[0] }
      })
      .catch((error) => {
        console.log(error)
      })
  }
}
</script>
