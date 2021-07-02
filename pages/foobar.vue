<template>
  <div class="container is-max-desktop">
    
    <div class="section homepage">
      <nav class="breadcrumb has-succeeds-separator" aria-label="breadcrumbs">
        <ul>
          <li>
            <nuxt-link to="/" style="margin: 0; padding: 0"> <a class="has-text-grey">Home</a> </nuxt-link>
          </li>
          <li>
            <nuxt-link to="/" style="margin: 0; padding: 0"> <a class="has-text-white-ter">FooBar</a> </nuxt-link>
          </li>
        </ul>
      </nav>

      <h5 class="title has-text-grey is-5 mb-1">Esercitazione 1</h5>
      <h1 class="title has-text-white-ter is-1">FooBar</h1>

      <div class="block input-items">
        <div class="input-items__item">
          <h5 class="title has-text-white-ter is-5 mb-1">Foo: </h5>
          <input v-model="foo" class="input ml-2" placeholder="Divisor number">
        </div>
        <div class="input-items__item">
          <h5 class="title has-text-white-ter is-5 mb-1">Bar: </h5>
          <input v-model="bar" class="input ml-2" placeholder="Divisor number">
        </div>
      </div>

      <button class="button is-dark" @click="startFooBar()">Start</button>

      <div class="block mt-5">
        <template v-for="item in numbers">
          <span class="tag is-medium" :class="item.class" :key="item">{{ item.value }}</span>
        </template>
      </div>
    </div>
    
  </div>
</template>


<script>
export default {
  data() {
    return {
      foo: null,
      bar: null,
      numbers: []
    }
  },
  methods: {
    startFooBar() {
      this.numbers = []

      for (var i=1; i<=100; i++) {
        const element = this.checkDivider(i)
        this.numbers.push(element);
      }
    },

    checkDivider(number) {
      const foo = parseInt(this.foo)
      const bar = parseInt(this.bar)

      if (number%foo === 0 && number%bar === 0)
        return { value: 'FooBar', class: 'is-warning' }

      if (number%foo === 0)
        return { value: 'Foo', class: 'is-success' }
      
      if (number%bar === 0)
        return { value: 'Bar', class: 'is-danger' }
      
      return { value: number, class: '' }
    }
  }
}
</script>