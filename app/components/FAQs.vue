<template>
   <Page>
        <StackLayout>
            <Label class="message" textWrap="true" :text="msg"/>
            <Button text="Return" @tap="goBack"></Button>
            <GridLayout>
                <FlexboxLayout flexDirection="column" justifyContent="space-around">
                    <ActivityIndicator :busy="isBusy" alignSelf="center" width="40" height="40" />
                </FlexboxLayout>
                <ListView for="p in pokemon" class="list-group">
                    <v-template>
                        <StackLayout class="list-group-item">
                            <Label :text="p.name" />
                            <Label :text="p.url" />
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
import axios from "axios";

    @Component({})
    export default class FAQs extends Vue {
        // @Prop()
            private msg: string;
        private pokemon: any[] = [];
        private isBusy: boolean = false;

        constructor() {
            super();
            this.msg = "Yet to build FAQs list";
        }

        beforeMount() {
            console.log('in beforeMount');
            this.initFetch();
            this.fetchTopFAQs();
        }

        goBack() {
            this.$navigateTo(App, {clearHistory: true});
        }

        toggleSpinner() {
            this.isBusy = !this.isBusy;
        }

        private async initFetch() {
            this.toggleSpinner();
            await this.fetchTopFAQs();
            this.toggleSpinner();
        }

        private async fetchTopFAQs(): Promise<any> {
            return axios.get('https://pokeapi.co/api/v2/pokemon/?limit=151')
                .then(response => {
                    console.log('pokemons', response.data);
                    this.pokemon = response.data.results;
                })
                .catch(error => {
                    console.log('Network call failed', error);
                });
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
