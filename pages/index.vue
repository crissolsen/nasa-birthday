<template>
  <b-container fluid>
    <h1 class="text-center mt-3 mb-3">Birthday Card Generator!</h1>
    <p class="text-center">
      Create a special QR Code to send a card to your friend.
    </p>
    <b-form @submit.prevent="onSubmit" v-if="show" class="mx-auto w-50">
      <b-form-group
        id="input-group-1"
        label="Recipient Email address:"
        label-for="input-1"
        description="We'll never share your email with anyone else."
      >
        <b-form-input
          id="input-1"
          v-model="form.email"
          type="email"
          placeholder="Enter email"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group
        id="input-group-2"
        label="Recipient Name:"
        label-for="input-2"
      >
        <b-form-input
          id="input-2"
          v-model="form.user"
          placeholder="Enter name"
          required
        ></b-form-input>
      </b-form-group>
      <b-form-group id="input-group-2" label="Your Name:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.recipient"
          placeholder="Your name"
          required
        ></b-form-input>
      </b-form-group>
      <b-form-group>
        <!-- <label for="example-datepicker">Choose a date</label>
        <b-form-datepicker
          id="example-datepicker"
          v-model="form.birthday"
          class="mb-2"
        ></b-form-datepicker> -->
        <label for="textarea">Birthday Message:</label>
        <b-form-textarea
          id="textarea"
          v-model="form.text"
          placeholder="Your birthday message..."
          rows="3"
          max-rows="6"
        ></b-form-textarea>
      </b-form-group>
      <b-button type="submit" variant="primary" class="text-center"
        >Submit</b-button
      >
    </b-form>
  </b-container>
</template>

<script>
export default {
  data() {
    return {
      show: true,
      form: {
        email: "",
        user: "",
        birthday: "",
        recipient: "",
        text: "",
      },
    };
  },
  methods: {
    async onSubmit() {
      var config = {
        method: "post",
        url: "https://nasa-birthday.homecode.workers.dev",
        headers: {
          "Content-Type": "application/json",
        },
        data: JSON.stringify(this.form),
      };

      const data = await this.$axios(config)
        .then(function (response) {
          console.log(response);
          alert("Message sent!")
          this.form = {}
        })
        .catch(function (error) {
          console.log(error);
        });
    },
  },
};
</script>
