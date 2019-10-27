<template>
    <nb-container>
        <!-- <AdMobBanner
            bannerSize="smartBannerPortrait"
            adUnitID="ca-app-pub-3940256099942544/6300978111"
            testDeviceID="EMULATOR" 
            servePersonalizedAds 
            :onDidFailToReceiveAdWithError="bannerError"
        /> -->
        <nb-content class="body-container">
                <button
                    :on-press="showAdd"
                    title="Show interstitial add"
                />
        </nb-content>
    </nb-container>
</template>

<script>
import { AdMobBanner, AdMobInterstitial } from 'expo-ads-admob'
export default {
    components: {
        AdMobBanner
    },
    props: {
        navigation: {
            type: Object
        },
    },
    mounted() {
        AdMobInterstitial.setAdUnitID('ca-app-pub-3940256099942544/1033173712'); // Test ID, Replace with your-admob-unit-id
        AdMobInterstitial.setTestDeviceID('EMULATOR');
        // AdMobInterstitial.addEventListener("interstitialDidLoad", () =>
        //     alert("interstitialDidLoad")
        // );
        // AdMobInterstitial.addEventListener("interstitialDidFailToLoad", () =>
        //     alert("interstitialDidFailToLoad")
        // );
        // AdMobInterstitial.addEventListener("interstitialDidOpen", () =>
        //     alert("interstitialDidOpen")
        // );
        // AdMobInterstitial.addEventListener("interstitialDidClose", () =>
        //     alert("interstitialDidClose")
        // );
        // AdMobInterstitial.addEventListener("interstitialWillLeaveApplication", () =>
        //     alert("interstitialWillLeaveApplication")
        // );
    },
    beforeDestroy() {
        // AdMobInterstitial.removeAllListeners();
    },
    methods: {
        bannerError(e) {
            alert(e)
        },
        async showAdd() {
            await AdMobInterstitial.requestAdAsync({ servePersonalizedAds: true});
            await AdMobInterstitial.showAdAsync();
        }
    },
}
</script>

<style>
    .body-container{
        padding: 10px;
    }
</style>
