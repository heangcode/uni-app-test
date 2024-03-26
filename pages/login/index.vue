<template>
  <view class="background-container">
    <view class="content">
      <!-- Banner Image -->
      <img
        class="banner-image"
        src="/static/images/login/banner.png"
        alt="banner image"
      />
      <!-- Container Card for Form -->
      <view class="container-card">
        <!-- Form Section -->
        <form @submit.prevent="onSubmit">
          <!-- Username Input Group -->
          <view class="input-group">
            <image class="input-icon" src="/static/images/login/account.png" />
            <input
              class="input-field"
              type="text"
              placeholder="请输入手机号"
              v-model="username"
            />
            <view
              v-if="username"
              class="input-clear"
              @click="clearInput('username')"
            >
              <text class="icon-clear">×</text>
            </view>
          </view>
          <!-- Password Input Group -->
          <view class="input-group">
            <image class="input-icon" src="/static/images/login/lock.png" />
            <input
              class="input-field"
              type="password"
              placeholder="请输入密码"
              v-model="password"
            />
            <view
              v-if="password"
              class="input-clear"
              @click="clearInput('password')"
            >
              <text class="icon-clear">×</text>
            </view>
          </view>
          <!-- Submit Button -->
          <button class="submit-button" type="submit">登录</button>
        </form>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
    clearInput(field) {
      this[field] = "";
    },
    onSubmit() {
      // This is where you would handle the form submission,
      // for example, by sending a request to a server.
      // The following is a mock function to represent this.
      this.login(this.username, this.password);
    },
    login(username, password) {
      // Replace with actual API call
      console.log(
        `Sending login for user ${username} with password ${password}`
      );
    },
  },
};
</script>

<style>
.background-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: url("/static/images/login/background.png") no-repeat center center;
  background-size: cover;
}

.content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.banner-image {
  margin-bottom: 24px;
  object-fit: cover;
  width: 400px;
}

.container-card {
  width: 90%;
  max-width: 350px;
  background-color: #ffffff;
  border-radius: 16px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  padding: 24px;
  box-sizing: border-box;
}

.input-group {
  position: relative;
}

.input-icon {
  position: absolute;
  left: 16px;
  top: 50%;
  transform: translateY(-50%);
  width: 24px;
  height: 24px;
}

.input-field {
  width: 100%;
  height: 50px;
  padding: 10px 16px 10px 48px; /* Left padding to account for the icon */
  margin-bottom: 16px; /* Space between input fields */
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box; /* Border and padding included in width */
}

.input-clear {
  position: absolute;
  right: 16px;
  top: 50%;
  transform: translateY(-50%);
  width: 24px;
  height: 24px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.icon-clear {
  font-size: 18px;
  color: #999;
  cursor: pointer;
}

.submit-button {
  width: 100%;
  background-color: #007aff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
</style>
