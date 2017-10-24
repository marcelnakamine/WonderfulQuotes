<template>
    <div class="container">
      <app-progress-bar :quoteCount="quotes.length" :maxQuotes="maxQuotes"></app-progress-bar>
      <app-new-quote @quoteAdded="newQuote"></app-new-quote>
      <app-quote-grid :quotes="quotes" @quoteDeleted="deleteQuote"></app-quote-grid>
      <div class="row">
        <div class="col-sm-12 text-center">
          <div class="alert alert-info">Info: Click on a Quote to delete it!</div>
          <div v-show="isToShowQuoteEmpty" class="alert alert-warning">Warning: Please write the quote to add.</div>
        </div>
      </div>
    </div>
</template>

<script>
import QuoteGrid from './components/QuoteGrid.vue';
import NewQuote from './components/NewQuote.vue';
import ProgressBar from './components/ProgressBar.vue';
import {eventBus} from './main';

export default {
  data: function() {
    return {
      isToShowQuoteEmpty: false,
      quotes: [
        'Just a Quote to see something'
      ],
      maxQuotes: 10
    }
  },
  methods: {
    newQuote(quote) {
      if(this.quotes.length >= this.maxQuotes) {
        return alert('Please delete Quotes first');
      }
      this.quotes.push(quote);
      this.isToShowQuoteEmpty = false;
    },
    deleteQuote(index) {
      this.quotes.splice(index,1);
    }
  },
  components: {
    appQuoteGrid: QuoteGrid,
    appNewQuote: NewQuote,
    appProgressBar: ProgressBar
  },
  created() {
    eventBus.$on('isQuoteEmpty', (data) => {
      this.isToShowQuoteEmpty = true;
    });
  }
}
</script>

<style>
</style>
