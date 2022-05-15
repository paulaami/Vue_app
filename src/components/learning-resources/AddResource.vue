<template>
  <base-dialog
    v-if="inputisInvalid"
    title="Invalid Input"
    @close="confrimError"
  >
    <template #default>
      <p>Unfortunately at least one input is invalid</p>
      <p>Please check all inputs</p>
    </template>
    <template #actions>
      <base-btn @click="confrimError">Okay</base-btn>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">title</label>
        <input type="text" id="title" ref="titleInput" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea id="description" rows="3" ref="descInput"></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <textarea id="link" rows="3" type="url" ref="linkInput"></textarea>
      </div>
      <div>
        <base-btn type="submit">Add resource</base-btn>
      </div>
    </form>
  </base-card>
</template>

//
<script>
// import { defineComponent } from '@vue/composition-api'

export default {
  inject: ['addResource'],
  data() {
    return {
      inputisInvalid: false,
    };
  },
  methods: {
    submitData() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescription = this.$refs.descInput.value;
      const enteredUrl = this.$refs.linkInput.value;

      if (
        enteredTitle.trim() === '' ||
        enteredDescription.trim() === '' ||
        enteredUrl === ''
      ) {
        this.inputisInvalid = true;
        return;
      }

      this.addResource(enteredTitle, enteredDescription, enteredUrl);
    },
    confrimError() {
      this.inputisInvalid = false;
    },
  },
};
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
