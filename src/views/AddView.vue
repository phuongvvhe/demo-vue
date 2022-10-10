<template>
  <a-form
      :model="formState"
      v-bind="layout"
      name="nest-messages"
      :validate-messages="validateMessages"
      @finish="onFinish"
  >
    <a-form-item :name="['valueAdd', 'username']" label="Username" >
      <a-input v-model:value="formState.valueAdd.username" />
    </a-form-item>
    <a-form-item :name="['valueAdd', 'email']" label="Email" :rules="[{ type: 'email' }]">
      <a-input v-model:value="formState.valueAdd.email" />
    </a-form-item>
    <a-form-item :name="['valueAdd', 'password']" label="Password" >
      <a-input v-model:value="formState.valueAdd.password" />
    </a-form-item>
    <a-form-item :name="['valueAdd', 'gender']" label="Gender">
      <a-input v-model:value="formState.valueAdd.gender" />
    </a-form-item>
    <a-form-item :name="['valueAdd', 'name']" label="Name">
      <a-textarea v-model:value="formState.valueAdd.name" />
    </a-form-item>
    <a-form-item :wrapper-col="{ ...layout.wrapperCol, offset: 8 }">
      <a-button type="primary" html-type="submit">Submit</a-button>
    </a-form-item>
  </a-form>
</template>
<script lang="ts">
import { defineComponent, reactive } from 'vue';
import axios from 'axios';
const baseUrl = 'http://localhost:8085/account';

export default defineComponent({

  setup() {
    const layout = {
      labelCol: { span: 8 },
      wrapperCol: { span: 16 },
    };

    const validateMessages = {
      // required: '${label} is required!',
      // types: {
      //   email: '${label} is not a valid email!',
      //   number: '${label} is not a valid number!',
      // },
      // number: {
      //   range: '${label} must be between ${min} and ${max}',
      // },
    };

    const formState = reactive({
      valueAdd: {
        username: '',
        name: '',
        password: '',
        gender: '',
        email: '',
        phone: '',
      },
    });
    const onFinish = (values: any) => {
      console.log('Success:', values);
        axios.post(`${baseUrl}/add`, this.formState.valueAdd)
          .then(response => {
            console.log(response)
          })
          .catch(error => {
            console.log(error);
          })
    };
    return {
      formState,
      onFinish,
      layout,
      validateMessages,
    };
  },
});
</script>
