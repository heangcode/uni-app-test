<template>
  <view class="container">
    <!-- Photos Cards -->
    <view class="card" v-for="photo in photos" :key="photo.id">
      <image
        class="card-image"
        :src="photo.thumbnailUrl"
        mode="aspectFill"
      ></image>
      <view class="card-content">
        <text class="card-title">{{ photo.id }}</text>
        <text class="card-text">{{ photo.title }}</text>
      </view>
    </view>

    <!-- Pagination Controls -->
    <view class="pagination-controls">
      <button @click="prevPage" :disabled="page <= 1">Prev</button>
      <text>{{ page }}</text>
      <button @click="nextPage" :disabled="page >= totalPhotos / perPage">
        Next
      </button>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      photos: [],
      page: 1,
      perPage: 10,
      totalPhotos: 5000,
    };
  },
  mounted() {
    this.fetchPhotos();
  },
  methods: {
    fetchPhotos() {
      const start = (this.page - 1) * this.perPage;
      const url = `https://jsonplaceholder.typicode.com/photos?_start=${start}&_limit=${this.perPage}`;
      uni.request({
        url: url,
        method: "GET",
        success: (res) => {
          if (res.statusCode === 200) {
            this.photos = res.data;
          } else {
            uni.showToast({
              title: "Error fetching photos",
              icon: "none",
            });
          }
        },
        fail: () => {
          uni.showToast({
            title: "Failed to fetch photos",
            icon: "none",
          });
        },
      });
    },
    prevPage() {
      if (this.page > 1) {
        this.page--;
        this.fetchPhotos();
      }
    },
    nextPage() {
      if (this.page < this.totalPhotos / this.perPage) {
        this.page++;
        this.fetchPhotos();
      }
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
  width: 100%;
}

.pagination-controls {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 20px;
}

.pagination-controls button {
  padding: 10px 15px;
  margin: 0 10px;
  background-color: #007aff;
  color: white;
  border: none;
  border-radius: 5px;
  font-weight: bold;
  cursor: pointer;
  outline: none;
}

.pagination-controls button:disabled {
  background-color: #cccccc;
  cursor: default;
}

.pagination-controls text {
  font-size: 16px;
  margin: 0 10px;
}

.card {
  padding: 16px;
  box-sizing: border-box;
  width: 90%; /* Responsive width */
  max-width: 400px; /* Maximum width */
  background-color: white;
  border-radius: 10px;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  align-items: center;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  margin-bottom: 20px;
  transition: transform 0.3s ease;
}

.card:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
}

.card-image {
  width: 80px; /* Adjusted for better proportions */
  height: 80px; /* Adjusted for better proportions */
  border-radius: 50%;
  object-fit: cover;
  margin-bottom: 10px;
}

.card-content {
  padding: 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
}

.card-title {
  font-size: 18px;
  font-weight: 700;
  color: #333;
  margin-bottom: 5px;
  text-align: center;
}

.card-text {
  font-size: 14px;
  color: #555;
  text-align: center;
  margin-bottom: 5px;
}

@media (max-width: 420px) {
  .card {
    width: 80%; /* Adjust width for small screens */
  }
}
</style>
