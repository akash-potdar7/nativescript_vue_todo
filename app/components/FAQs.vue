<template>
  <Label class="message" :text="msg"/>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

    @Component({})
    export default class FAQs extends Vue {
        @Prop() private msg: string;
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
