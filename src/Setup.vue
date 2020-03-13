<template>
  <view class="container">
    <view v-if="isLoading" :style="{flex: 1, justifyContent: 'center'}">
      <activity-indicator size="large" color="#0000ff" />
    </view>
    <app v-if="isLoaded" />
  </view>
</template>


<script>
import Vue from "vue-native-core";
import { VueNativeBase } from "native-base";
import App from "./Index.vue";
import * as Font from "expo-font";

// registering all native-base components to the global scope of the Vue
Vue.use(VueNativeBase);

export default {
  components: { App },
  data() {
    return {
      isLoaded: false,
      isLoading: true
    };
  },
  async mounted() {
    await Font.loadAsync({
      Roboto: require("../node_modules/native-base/Fonts/Roboto.ttf"),
      Roboto_medium: require("../node_modules/native-base/Fonts/Roboto_medium.ttf")
    });
    this.isLoading = false;
    this.isLoaded = true;
  }
};
</script>

<style>
.container {
  flex: 1;
}
</style>