<template>
  <div class="form">
    <div class="form__item">
      <label>Name</label>
      <base-input
        v-model="form.name"
        :placeholder="'Name'"
        @blur="isNameTouched = true"
        :class="{ error: isLengthError }"
      />
      <p v-if="isLengthError">Length should be 0 to 50</p>
    </div>
    <div class="form__item">
      <label>Email</label>
      <div class="form__item-btn">
        <base-input
          v-model="currentEmail"
          :placeholder="'Email'"
          @blur="isEmailTouched = true"
          :class="{ error: isEmailError }"
        />
        <base-button
          padding="0 20px"
          :height="'34px'"
          @click="addEmail(currentEmail)"
          >Add</base-button
        >
      </div>
      <div
        v-for="(item, index) in form.email"
        :key="index"
        class="form__item-list"
      >
        {{ item }} <a @click="removeEmail(index)">delete</a>
      </div>

      <p v-if="isEmailError">Please, enter correct email</p>
      <p v-if="!hasEmails" style="color: #000">Please, add some emails</p>
    </div>

    <base-button @click="sendLead" :width="'100%'">Send Lead</base-button>
  </div>
</template>

<script>
import BaseInput from "../components/BaseInput.vue";
import BaseButton from "../components/BaseButton.vue";

const emailCheckRegex = /^\S+@\S+\.\S+$/;

export default {
  components: {
    BaseInput,
    BaseButton,
  },
  data() {
    return {
      currentEmail: null,
      form: {
        name: "",
        email: [],
      },
      isEmailTouched: false,
      isNameTouched: false,
    };
  },
  computed: {
    isEmailValid() {
      return emailCheckRegex.test(this.currentEmail);
    },
    hasEmails() {
      return this.form.email.length;
    },
    isEmailError() {
      return !this.isEmailValid && this.isEmailTouched;
    },
    isLengthValid() {
      return this.form.name.length > 0 && this.form.name.length <= 50;
    },
    isLengthError() {
      return !this.isLengthValid && this.isNameTouched;
    },
  },

  methods: {
    addEmail() {
      this.isEmailTouched = true;
      if (!this.isEmailError) {
        this.form.email.push(this.currentEmail);
        this.currentEmail = "";
        this.isEmailTouched = false;
      }
    },
    removeEmail(index) {
      this.form.email.splice(index, 1);
    },
    sendLead() {
      if (this.hasEmails && this.isLengthValid) {
        alert(
          "Name: " +
            this.form.name +
            "|  Emails:  " +
            this.form.email.join(", ")
        );

        this.currentEmail = "";
        this.form.name = "";
        this.form.email = [];

        this.isNameTouched = false;
        this.isEmailTouched = false;
      } else {
        this.isNameTouched = true;
        this.isEmailTouched = true;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.form {
  margin: 75px auto;
  width: 500px;
  padding: 24px 48px;
  background: #ffffff;
  border-radius: 10px;
  -webkit-box-shadow: 0px 5px 10px 2px rgba(34, 60, 80, 0.2);
  -moz-box-shadow: 0px 5px 10px 2px rgba(34, 60, 80, 0.2);
  box-shadow: 0px 5px 10px 2px rgba(34, 60, 80, 0.2);
  &__item {
    &-btn {
      display: flex;
      justify-content: space-between;
      align-items: center;
      input {
        width: 80%;
      }
    }
    &-list {
      background: #d6d6d6;
      font-size: 10px;
      padding: 5px 10px;
      display: inline-block;
      border-radius: 5px;
      margin: 0 0 8px;
      a {
        cursor: pointer;
        color: blue;
        margin-left: 5px;
      }
    }
  }
  p {
    margin: 0 0 10px;
    font-size: 12px;
    color: #f5222d;
  }
}
.error {
  border-color: red;
}
</style>
