<template>
  <validation-provider
    v-slot="{ errors }"
    class="validation-provider"
    :name="field"
    rules="required"
    tag="div"
  >
    <input
      type="text"
      :name="name"
      :placeholder="field"
      :value="inputValue"
      class="input"
      :class="{ 'is-danger': errors.length >= 1 }"
      @input="input"
    />
    <p class="is-size-7 has-text-danger">{{ errors[0] }}</p>
  </validation-provider>
</template>

<script>
export default {
  model: {
    prop: 'inputValue',
    event: 'input',
  },
  props: {
    // 入力値
    inputValue: {
      type: String,
      required: true,
      default: '',
    },
    // Vee Validateのエラーフィールドとプレースホルダーのテキスト
    field: {
      type: String,
      required: true,
      default: '',
    },
    // input名
    name: {
      type: String,
      required: true,
      default: '',
    },
  },
  methods: {
    /**
     * 親に値を渡す
     * @param {Object} event
     */
    input(event) {
      this.$emit('input', event.target.value)
    },
  },
}
</script>

<style lang="scss" scoped>
.validation-provider {
  min-height: 3.8em;
}
</style>
