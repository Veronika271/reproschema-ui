<template>
  <div class="IntegerInput">
    <b-form ref="form" @submit="onSubmit" :novalidate="true">
      <b-form-group>
        <b-form-input ref="integerInput" v-model="input"
                      :class="{'is-invalid': !isValidEmail, 'is-valid': isValidEmail}">
        </b-form-input>
        <div class="invalid-feedback">
          {{ $t('invalid-email')}}
        </div>
      </b-form-group>
      <b-btn type="submit">{{ $t('submit-button')}}</b-btn>
    </b-form>
  </div>
</template>

<style>
</style>

<script>
export default {
  name: 'EmailInput',
  props: {
    'constraints': {},
    'init': {}
  },
  data() {
    return {
      input: null,
    };
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();
      this.$refs.form.className = 'was-validated';
      if (this.isValidEmail) {
        this.$emit('valueChanged', this.input);
      }
    },
    isValid(value) {
      if (/^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(value)) {
        return true;
      } return false;
    },
  },
  computed: {
    isValidEmail() {
      return this.isValid(this.input);
    },
  },
  mounted() {
    if (this.init) {
      this.input = this.init;
    }
  },
};
</script>
