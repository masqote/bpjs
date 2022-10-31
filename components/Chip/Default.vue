<template>
  <button
    class="px-3 py-1.5 rounded-md text-gray-600 hover:opacity-90 hover:shadow-md flex items-center space-x-2 transition hover:ease-in-out transform hover:scale-105 select-none flex-nowrap bg-gray-200"
    :class="{
      'bg-blue-600 text-white': selected,
    }"
    @click="onClick"
  >
    <div class="text-sm">{{ name }}</div>
    <div class="h-3 w-3 flex justify-center items-center">
      <img
        src="~/assets/svg/question.svg"
        class="h-full w-full"
        v-if="selected"
      />
      <img src="~/assets/svg/plus.svg" class="h-full w-full" v-else />
    </div>
  </button>
</template>

<script>
export default {
  props: {
    name: {
      default: 'default',
      type: String,
    },
    selected: {
      default: false,
      type: Boolean,
    },
  },
  methods: {
    onClick() {
      this.$emit('onClick')
    },
  },
}
</script>
