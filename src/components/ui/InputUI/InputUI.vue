<template>
  <div class="input-container">
    <label class="input-label">{{ label }}</label>
    <input
      class="input-field"
      :type="type"
      :value="modelValue"
      @input="updateInput"
      :placeholder="placeholder"
    />
  </div>
</template>

<script>
export default {
  props: {
    label: String,
    placeholder: String,
    modelValue: [String, Number],
    type: String,
  },
  data() {
    return {};
  },
  methods: {
    updateInput(e) {
      // this.$emit('update:modelValue', e.target.value) ???
      this.$emit('input', e.target.value)
    }
  },
};
</script>

<style scoped>
.input-container {
  font-family: 'Montserrat', sans-serif;
  display: flex;
  flex-direction: column;
  margin-top: 20px;
  margin-bottom: 10px;

}

.input-label {
  font-family: 'Montserrat', sans-serif;
  font-size: 14px;
  font-weight: 400;
  line-height: 16px;
  letter-spacing: 0;
  padding-left: 16px;
  text-align: left;
  margin-bottom: -20px;
  z-index: 1;
  color: #9B9B9B;
}

.input-field {
  font-family: 'Montserrat', sans-serif;
  font-size: 18px;
  font-weight: 500;
  line-height: 24px;
  letter-spacing: 0;
  height: 70px;
  text-align: left;
  padding: 8px 16px;
  border: 1px solid #ccc;
  border-radius: 4px;

}
</style>
