<template>
  <view class="container">
    <view class="header">
      <text class="headerText">About Pages</text>
    </view>
    <view class="content">
      <button class="uni-btn" @click="showMessage">{{ msg }}</button>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      msg: "This is a message from about",
    };
  },
  onLoad() {
    console.log("About page is loaded");
  },
  methods: {
    showMessage() {
      // This will show an alert when the button is clicked
      uni.showToast({
        title: "Welcome to the About Page!",
        duration: 2000,
      });
    },
  },
};
</script>

<style>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  height: 100%;
}

.header {
  margin-bottom: 20px;
}

.headerText {
  font-size: 24px;
  color: #333;
}

.uni-btn {
  background-color: #007aff;
  color: white;
  padding: 10px 20px;
  border-radius: 5px;
}
</style>
