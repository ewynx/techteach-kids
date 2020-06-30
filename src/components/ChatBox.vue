<template>
    <b-container fluid>
        <b-row align-h="end">
            <b-col cols="9" sm="7" md="5" lg="4" xl="3" id="chatbox">
                <b-row class="justify-content-start mb-2" align-v="center" id="sammi-title">
                    <b-col cols="3 pr-0">
                        <b-img fluid src="https://content.fortune.com/wp-content/uploads/2019/01/boo.jpg"
                               rounded="circle" alt="SammiBot" class="mb-1 mt-1"></b-img>
                    </b-col>
                    <b-col>
                        Chatea con Sammi
                    </b-col>
                </b-row>
                <b-container fluid id="chatarea" ref="chatArea" class="p-0">
                    <b-row v-for="(message, idx) in messages"
                           :key="idx"
                           v-bind:class="[ message.isSammi ? 'justify-content-start' : 'justify-content-end']"
                           class="m-0 mt-1"
                    >
                        <b-col v-if="!message.isTTClass"
                               class="p-2 message"
                               cols="auto"
                               v-bind:class="[ message.isSammi ? 'sammi' : 'client']"
                               align-self="end">
                            <span>{{ message.text }}</span>
                        </b-col>
                        <b-col v-if="message.isTTClass"
                               class="p-2"
                               cols="auto"
                               align-self="end">
                            <b-link class="tt-class"  :href="message.referral">
                                <b-img thumbnail :src="message.img"></b-img>
                            </b-link>
                        </b-col>
                    </b-row>

                </b-container>
                <b-input-group class="mt-3 mb-3">
                    <b-form-input type="text"
                                  v-model="message"
                                  @keyup.enter="sendMessage"></b-form-input>
                    <b-input-group-append>
                        <b-button @click="sendMessage">Enviar</b-button>
                    </b-input-group-append>
                </b-input-group>
            </b-col>
        </b-row>
    </b-container>
</template>

<script>
    import axios from "axios";

    export default {
        name: 'ChatBox',
        data: () => ({
            message: '',
            messages: []
        }),
        created() {
            this.messages.push({
                // TODO change. Esto es para empezar la conversacion.
                text: 'Hola, soy Sammi',
                isSammi: true
            });
        },
        methods: {
            thumbUrl(filename) {
                return require(`../assets/images/thumbnails/${filename}`);
            },
            sendMessage() {
                const message = this.message;
                this.messages.push({
                    text: message,
                    isTTClass: false,
                    isSammi: false
                });
                this.message = '';
                // TODO put into some config
                let baseURL = "https://api.dialogflow.com/v1/query?v=20150910";
                let token = "8103db856e484df6951b448f2ca9ce47";

                const headers = {
                    'Authorization': 'Bearer ' + token,
                };
                let data = {
                    query: message,
                    lang: 'en',
                    // TODO change to real sessionid
                    sessionId: '12345'
                };
                axios.post(baseURL, data, {headers})
                    .then(res => {
                        // Get the messages for Sammi and filter out the empty ones
                        let responseMessages = res.data.result.fulfillment.messages.filter(item => item.speech);
                        let responseMessagesCustom = res.data.result.fulfillment.messages.filter(item => item.payload);

                        if ( responseMessagesCustom.length > 0 ) {
                            responseMessagesCustom.forEach(async message => {
                                this.messages.push({
                                    text: message.payload.title,
                                    isTTClass: false,
                                    isSammi: true
                                });
                                this.messages.push({
                                    img: this.thumbUrl(message.payload.ttclass + '.jpg'), //TODO we should create a system to get img and referral for a specific "code class"
                                    referral: 'https://www.nos.nl', //TODO This would be a referral to our own website
                                    isTTClass: true,
                                    isSammi: true
                                });
                            });
                        } else {
                            responseMessages.forEach(async message => {
                                this.messages.push({
                                    text: message.speech,
                                    isTTClass: false,
                                    isSammi: true
                                });
                            });
                        }

                        this.$nextTick(() => {
                            let messageDisplay = this.$refs.chatArea;
                            messageDisplay.scrollTop = messageDisplay.scrollHeight;
                        });
                    });
            }
        }
    };
</script>

<style scoped lang="scss">
    #chatbox {
        box-shadow: 2px 2px 5px 2px rgba(0, 0, 0, 0.3);
        /*created en https://cssgradient.io/*/
        background: rgb(40, 44, 130);
        background: linear-gradient(351deg, rgba(40, 44, 130, 1) 0%, rgba(79, 83, 158, 1) 35%, rgba(165, 180, 229, 1) 100%);
    }

    #chatarea {
        max-height: 50vh;
        overflow: auto;

    }

    #sammi-title {
        background: #A5B4E5;
        text-align: start;
        color: white;
        font-size: 1.5em;
        font-weight: bold;
    }

    .container {
        border-color: black;
        border-width: 1px;
    }

    .message {
        border-radius: 8px;
    }

    .sammi {
        text-align: start;
        background: white;
        color: rgb(40, 44, 130);
    }

    .client {
        text-align: end;
        background: #F8EB7C;
    }

    .tt-class {
        background-color: transparent!important;
        padding: 0;
    }

    .btn {
        background-color: #A5B4E5;
        border-width: 0;
        color: black;
    }

    .form-control:focus {
        border-color: #ced4da;
        box-shadow: none;
    }
</style>
