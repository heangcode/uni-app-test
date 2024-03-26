<template>
  <view class="container">
    <form @submit.prevent="addItem">
      <view class="input-group">
        <text class="text-title">What do you need?</text>
        <input
          class="input"
          type="text"
          required
          placeholder="Eg. Apple"
          v-model="itemName"
        />
      </view>
      <view class="input-group">
        <text class="text-title">How many?</text>
        <input
          type="number"
          placeholder="Eg. 1"
          v-model.number="itemNumber"
          class="input"
        />
      </view>
      <button form-type="submit">Add item</button>
    </form>

    <view class="container-shoppingList">
      <text class="title">Shopping list:</text>
      <view class="list-container">
        <ul>
          <block v-for="(item, index) in shoppingList" :key="index">
            <li class="list-item">
              <view class="item-content">
                <text class="item-name">{{ item.name }}</text>
                <text class="item-number">Qty: {{ item.number }}</text>
              </view>
            </li>
          </block>
        </ul>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      itemName: "",
      itemNumber: "", // 默认为 1 以获得更好的用户体验
      shoppingList: [{ name: "apple", number: 10 }],
    };
  },
  methods: {
    addItem() {
      if (this.itemName && this.itemNumber > 0) {
        // 基本验证
        let item = {
          name: this.itemName,
          number: parseInt(this.itemNumber), // 确保数字存储为数字
        };
        this.shoppingList.push(item);
        this.itemName = "";
        this.itemNumber = ""; // 重置为默认值
      }
    },
  },
};
</script>

<style scoped>
.container {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 20px;
}

.input-group {
  margin-bottom: 15px;
}

.input {
  --input-focus: #2d8cf0;
  --font-color: #323232;
  --font-color-sub: #666;
  --bg-color: #fff;
  --main-color: #323232;
  width: 200px;
  height: 30px;
  border-radius: 5px;
  border: 2px solid var(--main-color);
  background-color: var(--bg-color);
  box-shadow: 4px 4px var(--main-color);
  font-size: 15px;
  font-weight: 600;
  margin-top: 10px;
  color: var(--font-color);
  padding: 5px 10px;
  outline: none;
}

.input::placeholder {
  color: var(--font-color-sub);
  opacity: 0.8;
}

.input:focus {
  border: 2px solid var(--input-focus);
}

.text-title {
  color: #323232;
  font-size: 20px;
  font-weight: 900;
}

.container-shoppingList {
  margin-top: 20px;
  width: 500rpx;
  padding: 10px;
  background-color: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.title {
  font-size: 18px;
  color: #333;
  font-weight: bold;
  margin-bottom: 10px;
}

.list-container ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

.list-item {
  margin-top: 20px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: #fff;
  margin-bottom: 8px;
  padding: 10px;
  border-radius: 5px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.item-content {
  display: flex;
  align-items: center;
}

.item-name {
  font-size: 16px;
  color: #007aff;
  margin-right: 15px;
}

.item-number {
  font-size: 14px;
  color: #666;
}

input,
button {
  width: 100px;
  padding: 0 2px;
  margin-top: 15px;
}

button {
  background-color: #007aff;
  color: white;
  border: none;
  border-radius: 10px;
}
</style>
