<template>
    <Page>
        <StackLayout>
            <Label :text="messageTitle" textWrap="true"></Label>
            <Label :text="actionMessage" textWrap="true"></Label>
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
    .page {
        align-items: center;
        flex-direction: column;
    }
</style>

