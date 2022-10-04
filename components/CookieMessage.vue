<template>
    <div class="bg-opacity" v-if="isOpen">
        <div class="cookie d-flex col-10 col-md-6 col-lg-5 col-xl-4"  >
            <div class="cookie_content d-flex container">
                <div class="banner__image">
                    <img src="path/of/your/image" alt="SET ALT">
                </div>
                <h5>Manage your Privacy</h5>
                <div name="message" class="slot">
                    {{ message }} <a href="/privacy" >cookies policy.</a> <!-- Add your link of privacy page -->
                </div>
            </div>
            <div class="button_cookie d-flex container">
                
                <div class="btn_fe btn_delete btn_shadow"  @click="deny()">
                    {{buttonTextDeny}}

                </div>

                <div class="btn_fe btn_shadow"  @click="accept()">
                    {{buttonTextAccept}}

                </div>
            </div>
        </div>
    </div>
</template>
<script>
import VueAnalytics from 'vue-analytics';
import Vue from 'vue';

export default {
    name: 'CookieMessage',
    props: {
        buttonTextAccept: {
            type: String,
            default: 'Accept'
        },
        buttonTextDeny: {
            type: String,
            default: 'Reject' 
        },
        message: {
            type: String,
            default: 'Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry\'s standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.' // COOKIE TEXT
        },
        position : {
            type: String,
            default: 'bottom'
        },

    },
    data() {
        return {
            isOpen : false,
            Gdpr : null
        }
    },
    mounted(){
        this.Gdpr = localStorage.getItem('GDPR:accepted')
        if(this.Gdpr == null) {
            this.isOpen = true;
        }

        if(this.Gdpr !== 'undefined' && this.Gdpr === 'true') {

            Vue.use(VueAnalytics, {
                id : '######', // ADD YOUR ANALYTICS ID 'EX. UA24837D'
                disabled: false,
                
            })

            window.dataLayer = window.dataLayer || [];
            function gtag(){dataLayer.push(arguments);}
            gtag('js', new Date());

            gtag('config', '######'); // ADD YOUR ANALYTICS ID 'EX. UA24837D'

        }else if(this.Gdpr !== 'undefined' && this.Gdpr === 'false') {

            Vue.use(VueAnalytics, {
                id : '######', // ADD YOUR ANALYTICS ID 'EX. UA24837D'
                disabled: true,
            })

        }
    },
    methods: {
        getGDPR() {
            if(process.client){
                return localStorage.getItem('GDPR:accepted', true);
            }
            
        },
        accept() {
            this.isOpen = false;
            localStorage.setItem('GDPR:accepted', true);
            
        },
        deny() {
            this.isOpen = false;
            localStorage.setItem('GDPR:accepted', false);
            
        }
        
    },
    
}
</script>
