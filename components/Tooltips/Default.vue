<template>
  <div class="group relative">
    <img src="~/assets/svg/question.svg" class="w-4 h-4" />
    <span
      class="justify-center absolute hidden group-hover:flex -left-[86px] -top-3 -translate-y-full w-48 px-2 py-1 bg-gray-700 rounded-lg text-center text-white text-sm after:content-[''] after:absolute after:left-1/2 after:top-[100%] after:-translate-x-1/2 after:border-8 after:border-x-transparent after:border-b-transparent after:border-t-gray-700"
      >{{ text }}</span
    >
  </div>
</template>

<script>
export default {
  props: {
    text: {
      default: 'Content here',
      type: String,
    },
  },
}
</script>
