<template lang="html">
  <div class="row">
    <form>
      <div class="col-sm-8 col-sm-offset-2 col-xs-12 col-md-6 col-md-offset-3">
        <label>Quote</label>
        <textarea class="form-control" name="quote" v-model="quote" rows="3" cols="80"></textarea>
      </div>
      <div class="col-sm-8 col-sm-offset-2 col-xs-12 col-md-6 col-md-offset-3">
        <button class="brn btn-primary" @click.prevent="createNew">Add Quote</button>
      </div>
    </form>
  </div>
</template>

<script>
import {eventBus} from '../main';

export default {
  data: function() {
    return {
      quote: ''
    };
  },
  methods: {
    createNew() {
      if (this.quote === '') {
        eventBus.$emit('isQuoteEmpty', this.quote);
      } else {
        this.$emit('quoteAdded', this.quote);
        this.quote = '';
      }
    }
  }
}
</script>

<style lang="css">

</style>
