<template>
  <div id="app">
    <Form v-slot="{form,meta}" :validation-schema="schema" @submit="onSubmit">
      <div class="flex flex-col w-80">
        <Field v-slot="{field,meta}" name="email" type="email">
          <label :class="{ 'bg-red': !testValid(meta) }">Email</label>
          <input :class="{ 'bg-red': !testValid(meta) }" v-bind="field">
        </Field>
        <ErrorMessage name="email">L'email n'est pas valide</ErrorMessage>
        <Field v-slot="{field,meta}" name="prenom" type="prenom">
          <label :class="{ 'bg-red': !testValid(meta) }">Prénom</label>
          <input :class="{ 'bg-red': !testValid(meta) }" v-bind="field">
        </Field>
        <ErrorMessage v-slot="{meta}" name="prenom">
          <div>
            Le prénom n'est pas valide
          </div>
        </ErrorMessage>
        <button>Soummetre</button>
      </div>
    </Form>
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
        email: string().min(2).required(),
        prenom: string().min(2).required(),
      })
    }
  },
  methods: {
    onSubmit(values) {
      console.log("Les values " + JSON.stringify(values));
    },
    testValid(meta) {
      return (meta.valid || meta.dirty === false);
    }
  },
};
</script>

<style scoped>
.bg-red {
  background-color: red;
}

* {
  display: block;
}
</style>
