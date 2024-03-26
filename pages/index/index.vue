<template>
  <view class="content">
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
export default {
  data() {
    return {
      title: "Hello",
      subtitle: "Welcome to vue uni-app!",
      navItems: [
        { label: "Go to About Pages !", path: "/pages/about/index" },
        { label: "Go to Fetch Data Pages !", path: "/pages/fetch/index" },
        { label: "Go to Shopping List !", path: "/pages/shopping/index" },
        { label: "Go to Login Pages !", path: "/pages/login/index" },
      ],
    };
  },
  methods: {
    navigateTo(path) {
      uni.navigateTo({ url: path });
    },
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
</style>
