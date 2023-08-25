<template>
  <div v-if="showModal" class="modal" @click="closeModal">
    <div class="modal-content" @click.stop>
      <div class="modal-header">
        <h3>{{modalName}}</h3>
        <button @click="closeModal" class="modal-close-btn">✕</button>
      </div>
      <div class="modal-body">
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ModalUI',
  props: {
    showModal: Boolean,
    modalName: String,
  },
  methods: {
    closeModal() {
      this.$emit('close');
    },
  },
};
</script>

<style>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}
.modal-content {
  background-color: white;
  padding: 15px;
  border-radius: 8px;
  min-width: 400px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  max-width: 80%;
  max-height: 80%;
  overflow: auto;
}
.modal-body{
  padding: 10px;
}
.modal-header{
  display: flex;
  justify-content: space-between;
}
.modal-close-btn{
  padding: 0;
  border: none;
  font-size: 15px;
  color: inherit;
  background-color: transparent;
  cursor: pointer;
}
</style>
