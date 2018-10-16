<template>
  <v-container fluid>
    <v-slide-y-transition mode="out-in">
      <v-layout column align-center>
        <v-progress-circular
        :rotate="360"
        :size="100"
        :width="15"
        :value="value"
        color="teal"
        >
          {{ value }}
        </v-progress-circular>
        <v-pagination v-model="page" :length="15" :total-visible="7" @input="next"></v-pagination>
      </v-layout>
    </v-slide-y-transition>
  </v-container>
</template>

<script>
import { VProgressCircular } from 'vuetify/es5/components/VProgressCircular';
import { VPagination } from 'vuetify/es5/components/VPagination';

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  components: {'v-progress-circular': VProgressCircular, 'v-pagination': VPagination},
  data() {
    return {
      interval: {},
      value: 0,
      page: 1
    }
  },
  beforeDestroy () {
    clearInterval(this.interval)
  },
  mounted () {
    this.interval = setInterval(() => {
      if (this.value >= 100) {
        return (this.value = 0)
      }
      this.value += 10
    }, 1000)
  },
  methods: {
    next (page) {
      this.value = parseInt(100/15*page);
    }
  }     
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
