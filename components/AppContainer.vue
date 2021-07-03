<template>
<div class="block apps__block">
  <div class="block mb-1 is-flex is-align-items-center is-flex-direction-row">
    <span class="mr-2">{{ icon }}</span>
    <nuxt-link :to="link">
      <h4 class="title has-text-white-ter is-4">{{ title }} ↗</h4>
    </nuxt-link>
  </div>
  <div class="block has-text-grey-light pl-2 pr-2 pb-2">
    {{ description }}
  </div>
</div>
</template>

<script>
export default {
  props: ['icon', 'title', 'link', 'description']
}
</script>