<template>
    <div class="navigation">
        <router-link to="/"><h1>News App</h1></router-link>
        <div class="center">
            This is a simple News App made using <strong class="red--text text--lighten-1">Vue.js</strong> and <strong class="red--text text--lighten-1">Vuetify</strong>.
        </div>
        <div class="sub-nav">
            <div class="back-button" >
                <v-btn @click="goBack" text>Back</v-btn>
            </div>
            <div class="profile">
                <router-link to="profile"> <v-btn text>Profile</v-btn></router-link>
            </div>
        </div>
    </div>  
</template>

<script>
export default {
    data() {
        return {
            showBack: false,

        }
    },
    methods: {
        goBack() {
            if(window.location.pathname == '/'){
                console.log('Already on home page')
            }
            else{
                this.$router.go(-1)
            }
        }
    }
}
</script>

<style scoped>

    .navigation{
        display: flex;
        flex-direction: column;;
        justify-content: center;
        align-items: center;
        min-height: 80px;
    }

    .center{
        text-align: center;
    }

    .sub-nav{
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        width: 100%;
        margin: auto 30px;
        padding: 10px;
    }


</style>