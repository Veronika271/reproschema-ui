<template>
  <div class="staticReadOnly">
    <div v-if="true">
      <b-btn @click="onSubmit"> Continue activity </b-btn>
    </div>
    <div v-else>
      <b-alert show>
        Parameter could not be retrieved at this time. Please contact "{{ contact }}" for further assistance.
      </b-alert>
    </div>
  </div>
</template>

<style>
</style>

<script>
import config from '../../../config';
export default {
  name: 'StaticReadOnly',
  props: {
    'constraints': {},
    'init': {},
    'result': {},
    'selected_language': {}
  },
  data() {
    return {
      contact: config.contact,
      input: '',
    };
  },
    methods: {
    onSubmit(e) {
      e.preventDefault();
      this.$emit('valueChanged', this.input);
    },
  },
  computed: {
    getPId() {
      return this.$store.getters.getParticipantId;
    },
  },
  mounted() {
    if (this.getPId) {
      this.input = this.getPId;
    }
    if (this.init) {
      this.input = this.init;
    }
  },
};
</script>
