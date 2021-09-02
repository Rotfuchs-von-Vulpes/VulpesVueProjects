<template>
  <div>
    <li>{{ description }}</li>
  </div>
</template>

<script>
export default {
  name: 'NestedToDo',
  props: {
    description: String,
  },
  watch: {
    checked: function() {
      this.$emit('check');
    }
  }
}
</script>