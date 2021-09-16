<template>
  <error-alert
    v-if="inputIsInvalid"
    title="Formulaire Incomplet"
    @close="confirmError"
  >
    <template #default>
      <p>Tous les champs ne sont pas renseignés</p>
      <p>Merci de remplir le formulaire en entier</p>
    </template>
    <template #action>
      <base-button @click="confirmError">Ok</base-button>
    </template>
  </error-alert>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Titre</label>
        <input id="title" name="title" type="text" ref="titleInput" />
      </div>
      <div class="form-control">
        <label for="description">Déscription</label>
        <textarea
          name="descritpion"
          id="description"
          cols="30"
          rows="10"
          ref="descInput"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="link">Lien</label>
        <input id="link" name="link" type="url" ref="linkInput" />
      </div>
      <div>
        <base-button type="submit">Ajouter</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
import BaseButton from './UI/BaseButton.vue';
import ErrorAlert from './UI/ErrorAlert.vue';
export default {
  components: { ErrorAlert, BaseButton },
  inject: ['addResource'],
  data() {
    return {
      inputIsInvalid: false
    };
  },
  methods: {
    submitData() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDesc = this.$refs.descInput.value;
      const enteredUrl = this.$refs.linkInput.value;

      if (
        enteredTitle.trim() === '' ||
        enteredDesc.trim() === '' ||
        enteredUrl.trim() === ''
      ) {
        this.inputIsInvalid = true;
      } else {
        this.addResource(enteredTitle, enteredDesc, enteredUrl);
      }
    },
    confirmError() {
      this.inputIsInvalid = false;
    }
  }
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
