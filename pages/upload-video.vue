<template>
  <div class="upload-container">
    <div class="u-card">
      <form @submit.prevent="handleSubmit">
        <div class="form-item">
          <label>Title</label>
          <input v-model="form.title" placeholder="Enter the title" required />
        </div>

        <div class="form-item">
          <label>Creator</label>
          <input v-model="form.creator" placeholder="Enter creator's name" required />
        </div>

        <div class="form-item">
          <label>File</label>
          <input type="file" ref="fileInput" @change="handleFileChange" required />
        </div>

        <button type="submit" class="submit-button">Upload</button>
      </form>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      form: {
        title: '',
        creator: '',
        media: null
      }
    };
  },
  methods: {
    handleFileChange(event) {
      const file = event.target.files[0];
      this.form.media = file;
    },
    async handleSubmit() {
      if (!this.form.media) {
        alert("Please select a file to upload.");
        return;
      }

      try {
        const formData = new FormData();
        formData.append('title', this.form.title);
        formData.append('creator', this.form.creator);
        formData.append('media', this.form.media);

        const response = await axios.post('http://localhost:8080/api/upload', formData, {
          headers: {
            'Content-Type': 'multipart/form-data'
          }
        });

        console.log('File uploaded successfully:', response.data);
      } catch (error) {
        console.error('Error uploading the file:', error.response?.data || error.message);
      }
    }
  }
};
</script>

<style scoped>
.upload-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 90vh;
}

.u-card {
  width: 400px;
  padding: 20px;
  background-color: #1e1b29; /* Fondo oscuro */
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
  color: aliceblue;
}

.form-item {
  margin-bottom: 1rem;
}

input {
  width: 100%;
  padding: 10px;
  margin-top: 5px;
  border-radius: 5px;
  border: 1px solid #ccc;
}

.submit-button {
  width: 100%;
  background-color: #f97316; /* Naranja vivo */
  color: #ffffff;
  padding: 10px 0;
  border: none;
  cursor: pointer;
  border-radius: 5px;
  font-weight: bold;
}

.submit-button:hover {
  background-color: #fb923c;
}
</style>
