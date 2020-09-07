<template>
    <div class="container-fluid mt-2" style="max-width: 400px">
        <b-form @submit="click" autocomplete="off">
            <b-row>
                <b-col cols="9">
                    <b-input :placeholder="$t('message')" id="in" v-model="input"></b-input>
                </b-col>
                <b-col cols="3">
                    <b-button id="but" type="submit" variant="primary">{{$t('send')}}</b-button>
                </b-col>
            </b-row>

        </b-form>
        <!--    <b-card class="mt-2" :header="$t('result')">-->
        <!--      {{$t(result.goal||"unknown")}}-->
        <!--      <p class="text-muted">Distanz: {{result.distance}}</p>-->
        <!--    </b-card>-->
        <Chatroom :items="messages"/>
    </div>
</template>

<script>
    // @ is an alias to /src
    import chatLogic from "edi.chatbot";
    import {addTranslations} from "edi.chatbot"
    import languages from "../lang"
    import Chatroom from "../components/Chatroom";

    export default {
        name: 'Home',
        data() {
            return {
                input: "",
                // result: "",
                messages: []
            }
        },
        components: {
            Chatroom
        },
        methods: {
            click(evt) {
                evt.preventDefault();
                this.messages.unshift({
                    text: this.input,
                    isSelf: true,
                    time: new Date()
                });
                this.messages.unshift({
                    text: this.$t(chatLogic.yesNoMaybe(this.input, this.$i18n.locale).goal),
                    isSelf: false,
                    time: new Date()
                });
                this.input = "";

            }
        },
        mounted() {
          addTranslations(languages);
          this.messages.unshift({
            text: this.$t("welcomeMessage"),
            isSelf: false,
            time: new Date()
          });
        }
    }
</script>

<style lang="css" scoped>

</style>
