<template>
  <div>
    <div class="container">
      <input
        type="text"
        placeholder="Введіть номер будинку"
        v-model="inputValue"
        @input="checkInput"
        :class="{
          input_valid: isInputValid,
          input_not_valid: !isInputValid && isInputValid != null,
        }"
      />
      <p class="validation_message_valid" v-if="isInputValid">
        Введений вами запис корректний
      </p>
      <p
        class="validation_message_invalid"
        v-if="!isInputValid && isInputValid != null"
      >
        Введений вами запис НЕ корректний
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "validatorInput",

  data() {
    return {
      inputValue: null,
      isInputValid: null,
    };
  },

  methods: {
    checkInput() {
      const pattern =
        /^[1-9]\d{0,2}[a-eа-дA-EА-Д]?([\-\/][1-9]?\d{0,2}?[a-eа-дA-EА-Д]?)?$/gm; //eslint-disable-line

      const regExp = new RegExp(pattern);

      if (regExp.test(this.inputValue) === true) {
        this.isInputValid = true;
      } else {
        this.isInputValid = false;
      }
      if (this.inputValue.length == 0) {
        this.isInputValid = null;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  input {
    margin: 20px auto;
    display: block;
    width: 100%;
    max-width: 250px;
    height: 100%;
    height: 35px;
    font-size: 18px;
    padding: 5px;
    border-radius: 3px;
    border: 3px solid black;
    outline: none;

    &:focus {
      outline: none;
    }
  }

  .input_valid {
    border: 3px solid rgb(33, 207, 33);
    &:focus {
      border: 3px solid rgb(33, 207, 33);
      border-radius: 3px;
    }
  }
  .input_not_valid {
    border: 3px solid red;
    &:focus {
      border: 3px solid red;
    }
  }

  .validation_message_valid {
    color: rgb(34, 180, 34);
  }

  .validation_message_invalid {
    color: red;
  }
}
</style>
