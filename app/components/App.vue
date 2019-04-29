<template>
    <Page>
        <GridLayout>
            <FAQs :msg="msg" />
        </GridLayout>
    </Page>
</template>

<script lang="ts">

import { Component, Prop, Vue } from "vue-property-decorator";
import FAQs from './FAQs.vue';

  @Component({
    components: {
        FAQs
    }  
  })
  export default class App extends Vue {
    data() {
      return {
        msg: 'Welcome to Airim Native-app!'
      }
    }
  }
</script>
