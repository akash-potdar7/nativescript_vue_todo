<template>
   <Page>
        <StackLayout>
            <Label class="message" textWrap="true" :text="msg"/>
            <Button text="Return" @tap="goBack"></Button>
            <GridLayout>
                <ListView for="p in pokemon" class="list-group">
                    <v-template>
                    <StackLayout class="list-group-item">
                        <Label :text="p.name" />
                    </StackLayout>
                    </v-template>
                </ListView>
            </GridLayout>
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
        private pokemon: any[] = [];

        constructor() {
            super();
            this.msg = "Yet to build FAQs list";
        }

        beforeMount() {
            console.log('beforeUpdate')
        }

        goBack() {
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
