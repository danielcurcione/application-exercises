<template>
<div>
  <nav class="breadcrumb" aria-label="breadcrumbs">
    <ul>
      <li v-for="page in pages" :key="page">
        <nuxt-link to="./home" style="margin: 0; padding: 0"> <a class="has-text-grey">{{ page | capitalize}}</a> </nuxt-link>
      </li>
    </ul>
  </nav>

  <h5 class="title has-text-grey is-5 mb-1">{{ subtitle }}</h5>
  <h1 class="title has-text-white-ter is-1">{{ title }}</h1>
</div>
</template>

<script>
export default {
  props: ['title', 'subtitle', 'link'],
  data() {
    return {
      pages: this.link.split('/')
    }
  },
  filters: {
    capitalize: function (value) {
      if (!value) return ''
      value = value.toString()
      return value.charAt(0).toUpperCase() + value.slice(1)
    }
  }
}
</script>