<template>
  <teleport to="body">
    <div @click="$emit('close')">
      <base-dialog v-if="isInputInvalid" title="Invalid Input" @close="confirmError">
        <template #default>
          <p>All inputs are necessary</p>
          <p>Make sure you have entered some value</p>
        </template>
        <template #actions>
          <base-button @click="confirmError">Okay</base-button>
        </template>
      </base-dialog>
      <base-card>
        <form @submit.prevent="onFormSubmit">
          <div class="form-control">
            <label for="title">Title</label>
            <input type="text" name="title" id="title" @change="onType" />
          </div>
          <div class="form-control">
            <label for="description">Description</label>
            <textarea
              name="description"
              id="description"
              @change="onType"
              cols="30"
              rows="10"
            ></textarea>
          </div>
          <div class="form-control">
            <label for="url">Link</label>
            <input type="url" name="link" id="url" @change="onType" />
          </div>
          <div>
            <base-button type="submit"> Add Resource </base-button>
          </div>
        </form>
      </base-card>
    </div>
  </teleport>
</template>
<script>
export default {
  inject: ["addResource"],
  data() {
    return {
      isInputInvalid: false,
      formData: {
        title: null,
        description: null,
        link: null,
      },
    };
  },
  methods: {
    onType(event) {
      if (event.target.name !== "") {
        this.formData[`${event.target.name}`] = event.target.value;
      }
    },
    confirmError() {
      this.isInputInvalid = false;
    },
    onFormSubmit() {
      for (const key in this.formData) {
        if (!this.formData[key]) {
          this.isInputInvalid = true;
          break;
        }
      }
      if (!this.isInputInvalid) {
        this.addResource(this.formData);
      }
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
