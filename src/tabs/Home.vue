<template>
  <nb-container>
    <nb-content>
      <view :style="{ flex: 1, justifyContent: 'center', alignItems: 'center' }">
        <image
          :style="{width: 300, height: 300}"
          :source="require('../../assets/LOGO-HEXAGONO-512X512.png')"
        />
      </view>
      <view :style="{ flex:1 }">
        <touchable-opacity
          v-for="test in tests"
          :key="test.id"
          class="btn"
          @press="onButtonPressed(test.route)"
        >
          <nb-text :style="{ color: 'white', textAlign: 'center' }">Score MAMÁ</nb-text>
        </touchable-opacity>
      </view>
      <view>
        <touchable-opacity class="btn-disabled" :disabled="true">
          <nb-text :style="{ color: 'gray', textAlign: 'center' }">Edad Gestacional</nb-text>
        </touchable-opacity>
      </view>
      <view>
        <touchable-opacity class="btn-disabled" :disabled="true">
          <nb-text :style="{ color: 'gray', textAlign: 'center' }">Claves Obstétricas</nb-text>
        </touchable-opacity>
      </view>
    </nb-content>
  </nb-container>
</template>

<script>
import { AdMobInterstitial } from "expo-ads-admob";
import { Platform } from "react-native";
export default {
  props: {
    navigation: {
      type: Object
    }
  },
  data() {
    return {
      tests: [{ id: 0, name: "Score Mama", route: "scoreMama" }],
      navigateRoute: "",
      interIdiOS: "ca-app-pub-1500612778036594/5284346966",
      interIdAndroid: "ca-app-pub-1500612778036594/5619388887",
      // test IDs
      // interIdiOS: "ca-app-pub-3940256099942544/4411468910",
      // interIdAndroid: "ca-app-pub-3940256099942544/1033173712",
      interUnitId: ""
    };
  },
  beforeMount() {
    this.interUnitId =
      Platform.OS === "ios" ? this.interIdiOS : this.interIdAndroid;
  },
  mounted() {
    AdMobInterstitial.setAdUnitID(this.interUnitId);
    this.requestAd();
    AdMobInterstitial.addEventListener("interstitialDidClose", this.requestAd);
    // AdMobInterstitial.addEventListener("interstitialDidFailToLoad", () =>
    //   alert("interstitialDidFailToLoad")
    // );
  },
  beforeDestroy() {
    AdMobInterstitial.removeAllListeners(
      "interstitialDidClose",
      this.requestAd
    );
  },
  methods: {
    // handler() {
    //   this.requestAd();
    //   // this.navigate();
    // },
    navigate(route) {
      this.navigation.navigate(route);
    },
    async requestAd() {
      await AdMobInterstitial.requestAdAsync({ servePersonalizedAds: true });
    },
    async showAd() {
      // await AdMobInterstitial.requestAdAsync({ servePersonalizedAds: true });
      await AdMobInterstitial.showAdAsync();
    },
    onButtonPressed(route) {
      this.showAd();
      // this.navigateRoute = route;
      this.navigate(route);
    }
  }
};
</script>

<style>
.header-container {
  margin-top: 24px;
}
.container {
  flex: 1;
  justify-content: center;
  align-content: center;
}
.btn {
  flex: 1;
  margin: 10px;
  padding: 10px;
  background-color: #007bff;
  border-radius: 10px;
}
.btn-disabled {
  flex: 1;
  margin: 10px;
  padding: 10px;
  background-color: lightsteelblue;
  border-radius: 10px;
}
</style>
