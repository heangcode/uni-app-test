<template>
  <view class="content" :key="locale">
    <!-- Add a picker to switch languages -->
    <picker
      mode="selector"
      :range="languageOptions"
      :value="selectedLanguageIndex"
      @change="onLanguageChange"
    >
      <view class="language-picker">
        <image :src="selectedFlag" class="flag-icon"></image>
        <text>{{ selectedLanguageLabel }}</text>
      </view>
    </picker>
    <image class="logo" src="/static/logo.png"></image>
    <view class="text-area">
      <text class="title">{{ title }}</text>
      <text class="subtitle">{{ subtitle }}</text>
      <view class="nav-list">
        <ul
          v-for="(item, index) in navItems"
          :key="index"
          @click="navigateTo(item.path)"
          class="nav-item"
        >
          <li>{{ item.label }}</li>
        </ul>
      </view>
    </view>
  </view>
</template>

<script>
import { messages } from "../../utils/i18n";

export default {
  data() {
    return {
      locale: "en", // default locale
      selectedLanguageIndex: 0, // Index for the picker, 0 for English, 1 for Chinese
      languageOptions: [
        { label: "English", value: "en", flag: "/static/images/flags/usa.png" },
        { label: "中文", value: "cn", flag: "/static/images/flags/china.png" },
      ],
    };
  },
  computed: {
    selectedFlag() {
      return this.languageOptions[this.selectedLanguageIndex].flag;
    },
    selectedLanguageLabel() {
      return this.languageOptions[this.selectedLanguageIndex].label;
    },
    title() {
      return messages[this.locale].title;
    },
    subtitle() {
      return messages[this.locale].subtitle;
    },
    navItems() {
      return [
        { label: messages[this.locale].about, path: "/pages/about/index" },
        { label: messages[this.locale].fetchData, path: "/pages/fetch/index" },
        {
          label: messages[this.locale].shoppingList,
          path: "/pages/shopping/index",
        },
        { label: messages[this.locale].login, path: "/pages/login/index" },
      ];
    },
  },
  methods: {
    onLanguageChange(event) {
      const chosenIndex = event.detail.value;
      this.selectedLanguageIndex = chosenIndex;
      const chosenLanguage = this.languageOptions[chosenIndex].value;
      this.switchLocale(chosenLanguage);
    },
    navigateTo(path) {
      uni.navigateTo({ url: path });
    },
    switchLocale(newLocale) {
      this.locale = newLocale;
      uni.setStorageSync("preferredLanguage", this.locale); // Store the preferred language
      console.log("Locale switched to:", this.locale); // Check if this logs correctly
    },
  },
  onShow() {
    // Check the preferred language or default to English
    const preferredLanguage = uni.getStorageSync("preferredLanguage") || "en";
    this.locale = preferredLanguage;
  },
};
</script>

<style>
.content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.logo {
  height: 200rpx;
  width: 200rpx;
  border-radius: 100px;
  margin-top: 50rpx;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 50rpx;
}

.text-area {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-content: center;
  text-align: center;
}

.title {
  font-size: 56rpx;
  font-weight: 900;
  color: black;
}

.subtitle {
  font-size: 20px;
  color: black;
}

.nav-list {
  margin-top: 20px;
}

.nav-item {
  padding: 10px;
  margin: 5px 0;
  border-radius: 5px;
  cursor: pointer;
  width: 100%;
  border-radius: 10px;
  text-align: left;
}

.nav-item:hover {
  text-decoration: underline;
  color: blue;
}

.language-picker {
  display: flex;
  align-items: center;
}

.flag-icon {
  width: 24px; /* or the size you prefer */
  height: 24px; /* or the size you prefer */
  margin-right: 8px;
}
</style>
