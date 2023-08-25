<template>
  <div class="select-container">
    <label class="select-label">{{ label }}</label>
    <select class="select-field" :value="modelValue" @change="updateSelect">
      <option v-for="option in options" :key="option.value" :value="option.value">{{ option.label }}</option>
    </select>
  </div>
</template>

<script>
export default {
  props: {
    label: String,
    options: Array,
    modelValue: [String, Number],
  },
  methods: {
    updateSelect(e) {
      this.$emit('input', e.target.value);
    }
  },
};
</script>

<style>
.select-container {
  font-family: 'Montserrat', sans-serif;
  display: flex;
  flex-direction: column;
  margin-top: 20px;
  margin-bottom: 10px;
}

.select-label {
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

.select-field {
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
