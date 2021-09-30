<template>
  <div id="app">
    <Form v-slot="{form,meta}" :validation-schema="schema" @submit="onSubmit">
      <div class="flex flex-col w-80">
        <Field v-slot="{field,meta}" name="email" type="email">
          <label>Email</label>
          <input :class="{ 'bg-red': !testValid(meta) }" autocomplete="off" v-bind="field">
          <ErrorMessage :as="'span'" name="email">L'email n'est pas valide</ErrorMessage>
          <div>Meta champ email</div>
          <pre>{{ meta }}</pre>
        </Field>
        <hr>
        <Field v-slot="{field,meta}" name="prenom" type="prenom">
          <label>Prénom</label>
          <input :class="{ 'bg-red': !testValid(meta) }" autocomplete="off" v-bind="field">
          <ErrorMessage :as="'span'" name="prenom">Le prénom n'est pas valide</ErrorMessage>
          <div>Meta champ prenom</div>
          <pre>{{ meta }}</pre>
        </Field>
        <hr>
        <button>Soummetre</button>
        <hr>
        <div>Meta formulaire</div>
        <pre>{{ meta }}</pre>
      </div>
    </Form>
    <hr>
    Résultat soumettre : {{ formValues }}
  </div>
</template>
<script>
import {ErrorMessage, Field, Form} from 'vee-validate';
import {object, string} from "yup"

export default {
  components: {
    Form,
    Field,
    ErrorMessage,
  },
  data() {
    return {
      schema: object({
        email: string().email().required(),
        prenom: string().min(2).required(),
      }),
      formValues: ''
    }
  },
  methods: {
    onSubmit(values) {
      this.formValues = JSON.stringify(values);
    },
    testValid(meta) {
      return (meta.valid || meta.touched === false);
    }
  },
};
</script>

<style scoped>
* {
  display: block;
}

.bg-red {
  border-color: red;
}

span[role="alert"] {
  color: red;
}
</style>
