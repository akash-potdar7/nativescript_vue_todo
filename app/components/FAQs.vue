<template>
    <Page class="page" actionBarHidden="true" backgroundSpanUnderStatusBar="true">
		<GridLayout orientation="vertical" width="100%" height="100%" columns="*" rows="*,auto">
			<StackLayout col="0" row="0" backgroundColor="#f8f8f8">
                <Label class="font-weight-bold" marginTop="10" paddingLeft="10" fontSize="20" color="#333333" :text="headline"></Label>
                <FlexboxLayout v-if="isBusy" flexDirection="column" justifyContent="space-around">
                    <ActivityIndicator :busy="isBusy" alignSelf="center" width="40" height="40" />
                </FlexboxLayout>
                <ListView class="list-group" v-for="(faq, index) in faqs" :key="index" marginTop="10">
                    <v-template>
                        <GridLayout orientation="horizontal" class="list-group-item" rows="auto" columns="auto,*,auto">
                            <StackLayout col="1" row="0" marginLeft="16" padding="8">
                                <Label marginTop="4" textWrap="true" paddingRight="4" :text="faq.question" class="list-group-item-heading font-weight-bold" color="#333333"></Label>
                                <HtmlView textWrap="true" class="p-10" marginTop="4" :html="faq.answer" color="#999999"></HtmlView>
                                <FlexboxLayout margin="0" padding="0" flexDirection="row" justifyContent="space-around" alignItems="flex-start">
                                    <Button borderRadius="10" fontSize="12" color="#333333" v-for="(action, key) in faq.actions" :key="key" :text="action.label" @tap="onCTAClick(faq.actions[0])"/>
                                </FlexboxLayout>
                            </StackLayout>
                        </GridLayout>
                    </v-template>
                </ListView>
            </StackLayout>
		</GridLayout>
	</Page>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import App from './App.vue';
import axios from "axios";
import * as utils from "tns-core-modules/utils/utils";

    @Component({})
    export default class FAQs extends Vue {
        
        private faqs: any[] = [];
        private isBusy: boolean = false;
        private headline: string;

        constructor() {
            super();
            this.headline = "Frequently asked questions";
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

        onCTAClick(action: any) {
            utils.openUrl(action.web_url)
        }

        private async initFetch() {
            this.toggleSpinner();
            await this.fetchTopFAQs();
            this.toggleSpinner();
        }

        private async fetchTopFAQs(): Promise<any> {
            return axios.get('../assets/faqs.json')
                .then(response => {
                    const faqs = {
                                "top_faqs": [
                                {
                                    "id": 117,
                                    "question": "Who are Airim's founders?",
                                    "answer": "<p>If you run an agency, or handle multiple websites, you can sign up with different emails for each account. Once you have done that, just write to hi@airim.co and we will link all your accounts, so that you can login with one email address for all accounts.</p>",
                                    "tags": [
                                    "cxo",
                                    "cto",
                                    "ceo",
                                    "directors"
                                    ],
                                    "account_id": 1059401424129564,
                                    "category_id": 1517,
                                    "rank": null,
                                    "actions": [
                                        {
                                            "link_type": "web_url",
                                            "web_url": "https://www.linkedin.com/company/13299648/admin/",
                                            "action_id": 1151,
                                            "widget_id": null,
                                            "label": "View Team Page"
                                        },
                                        {
                                            "link_type": "web_url",
                                            "web_url": "https://app.airim.co/home/faqsManager/",
                                            "action_id": 1308,
                                            "widget_id": null,
                                            "label": "Import Now"
                                        }
                                    ]
                                },
                                {
                                    "id": 2998,
                                    "question": "Can I integrate multiple knowledge bases within the same subscription?",
                                    "answer": "<p><span style=\"color: rgb(74, 74, 74);\">Yes, it is possible. Simply click Import in your Content Manager and add your knowledge bases one-by-one. You can also add more FAQs one-by-one manually after importing your entire knowledge base content.</span></p>",
                                    "tags": [],
                                    "account_id": 1059401424129564,
                                    "category_id": 2217,
                                    "rank": null,
                                    "actions": [
                                        {
                                            "link_type": "web_url",
                                            "web_url": "https://app.airim.co/home/faqsManager/",
                                            "action_id": 1308,
                                            "widget_id": null,
                                            "label": "Import Now"
                                        }
                                    ]
                                },
                                {
                                    "id": 2874,
                                    "question": "How do I create multiple accounts?",
                                    "answer": "<p>If you run an agency, or handle multiple websites, you can sign up with different emails for each account. Once you have done that, just write to hi@airim.co and we will link all your accounts, so that you can login with one email address for all accounts.</p>",
                                    "tags": [],
                                    "account_id": 1059401424129564,
                                    "category_id": 2217,
                                    "rank": null,
                                    "actions": [
                                        {
                                            "link_type": "web_url",
                                            "web_url": "https://app.airim.co/signup",
                                            "action_id": 1152,
                                            "widget_id": null,
                                            "label": "Start Now for Free"
                                        }
                                    ]
                                },
                                {
                                    "id": 99,
                                    "question": "What is Airim used for?",
                                    "answer": "<p>Airim saves time for your users by surfacing the right FAQ for them at the right time.</p><p>Website visitors love interacting with Airim as it helps them explore websites with ease. And CXOs love it because it saves time for their customers.</p><p>Airim's analytics is immensely powerful, and product marketers use it to know what their customers are looking for, what excites them and what makes them lose interest.</p>",
                                    "tags": [
                                    "What is Airim",
                                    "what is the use"
                                    ],
                                    "account_id": 1059401424129564,
                                    "category_id": 1517,
                                    "rank": null,
                                    "actions": [
                                        {
                                            "link_type": "web_url",
                                            "web_url": "https://app.airim.co/signup",
                                            "action_id": 300,
                                            "widget_id": 0,
                                            "label": "Start Now for Free"
                                        }
                                    ]
                                },
                                {
                                    "id": 115,
                                    "question": "How long will it take to set up?",
                                    "answer": "<p>Less than a minute actually. Just sign up, provide your knowledge base URL and embed your unique Airim in your website or product.</p>",
                                    "tags": [
                                    "time"
                                    ],
                                    "account_id": 1059401424129564,
                                    "category_id": 1517,
                                    "rank": null,
                                    "actions": [
                                        {
                                            "link_type": "web_url",
                                            "web_url": "https://app.airim.co/signup",
                                            "action_id": 301,
                                            "widget_id": 0,
                                            "label": "Start Now for Free"
                                        }
                                    ]
                                }
                                ]
                            };
                    this.faqs = faqs.top_faqs;
                    console.log('faqs', response.data);
                })
                .catch(error => {
                    console.log('Network call failed', error);
                });
        }

    }
</script>
