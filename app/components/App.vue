<template>
    <Page>
        <StackLayout>
            <Label :text="messageTitle"></Label>
            <Label :text="actionMessage"></Label>
            <Button text="See FAQs" @tap="routeToFAQsPage"></Button>
        </StackLayout>
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

    messageTitle: string;
    actionMessage: string = 'Go to FAQs';

    beforeMount() {
        this.messageTitle =  'Welcome to Airim Native-app!';
        this.actionMessage = 'Go to FAQs';
    }

    routeToFAQsPage() {
        this.$navigateTo(FAQs, { clearHistory: true });
    }

  }
</script>
<style lang="scss" scoped>
</style>

