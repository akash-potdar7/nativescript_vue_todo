<template>
   <Page>
        <StackLayout>
            <Label class="message" textWrap="true" :text="msg"/>
            <Button class="btn btn-primary" text="Return" @tap="goBack"></Button>
        </StackLayout>
    </Page>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import App from './App.vue';

    @Component({})
    export default class FAQs extends Vue {
        // @Prop()
        private msg: string;

        constructor() {
            super();
            this.msg = "Yet to build FAQs list";
        }

        goBack() {
            console.log('laka', 'routing back to Home');
            this.$navigateTo(App, {clearHistory: true});
        }
    }
</script>
<style lang="scss" scoped>
    .message {
        vertical-align: center;
        text-align: center;
        font-size: 20;
        color: #333333;
    }
</style>
