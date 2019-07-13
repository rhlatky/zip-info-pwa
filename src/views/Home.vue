<template>
    <div class="ion-page">
        <ion-header>
            <ion-toolbar>
                <ion-title>ZipInfo</ion-title>
            </ion-toolbar>
        </ion-header>
        <ion-content class="ion-padding">
            <zip-search v-on:get-zip="getZipInfo"></zip-search>
            <zip-info v-bind:info="info"></zip-info>
            <clear-info v-bind:info="info" v-on:clear-info="clearInfo"></clear-info>
        </ion-content>
    </div>
</template>

<script>
    // @ is an alias to /src
    import ZipSearch from '../components/ZipSearch'
    import ZipInfo from '../components/ZipInfo'
    import ClearInfo from '../components/ClearInfo'

    export default {
        name: "home",
        components: {
            ZipSearch,
            ZipInfo,
            ClearInfo
        },
        data() {
          return {
              info: null
          };
        },
        methods:{
            getZipInfo: async function (zip) {
                const res = await fetch('https://api.zippopotam.us/us/' + zip);
                if(res.status === 404){
                    this.showAlert();
                }
                 this.info = await res.json();
            },
            showAlert: function () {
                return this.$ionic.alertController.create({
                    header: "Not Valid",
                    message: "Please enter a valid US zipcode",
                    buttons: ["OK"]
                }).then(a => a.present());
            },
            clearInfo: function () {
                this.info = null;
            }
        }
    };
</script>
