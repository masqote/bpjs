<template>
  <div class="w-full">
    <div>
      <select
        v-if="resources"
        v-model="valueSelect"
        :disabled="disabled"
        class="appearance-none w-full py-1.5 px-4 form-base"
        :class="{
          'form-disabled': disabled,

          'form-error': validate.error || error,
        }"
        @change="selectedData"
      >
        <option value="" valueSelect>{{ placeholder }}</option>
        <option
          v-for="resource in resources"
          :key="resource.id"
          :value="resource.id"
        >
          {{ resource.name }}
        </option>
      </select>
    </div>
    <span v-if="validate.error" class="text-red-600 font-semibold text-xs mt-1">
      {{ validate.msg }}
    </span>
  </div>
</template>

<script>
export default {
  props: {
    resources: {
      type: Array,
      default: () => [],
    },
    disabled: {
      default: false,
      type: Boolean,
    },
    required: {
      default: false,
      type: Boolean,
    },
    error: {
      default: false,
      type: Boolean,
    },
    value: {
      default: null,
    },
    placeholder: {
      default: null,
      type: String,
    },
  },
  data() {
    return {
      valueSelect: this.value ?? '',
      validate: {
        msg: null,
        error: false,
      },
    }
  },
  watch: {
    value(val) {
      val && (this.valueSelect = val)
    },
    valueSelect(val) {
      if (this.required && val === '') {
        this.validate.error = true
        this.validate.msg = 'Harap pilih salah satu'
      } else {
        this.validate.error = false
        this.validate.msg = null
      }
    },
  },
  methods: {
    selectedData() {
      this.$emit('input', this.valueSelect)
    },
  },
}
</script>
