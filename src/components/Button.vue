<template>
  <div>
    <v-btn dark  @click="onClick" :style="{ backgroundColor: color }">{{
      text
    }}</v-btn>
  </div>
</template>

<script>
export default {
  name: 'Button',
  props: {
    text: String,
    color: String
  },
  methods: {
    onClick () {
      this.$emit('btn-click')
    }
  }
}
</script>
