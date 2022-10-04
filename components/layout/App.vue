<template>

    <CookieMessage v-if="this.$route.fullPath != '/privacy'" />
       
</template>

<script>
import CookieMessage from '../CookieMessage.vue';

    export default {
        components: {
            CookieMessage
        },
    }
</script>
