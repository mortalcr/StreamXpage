<template>
  <div class="upload-container">
    <UCard>
      <UForm @submit.prevent="handleSubmit">
        <UForm-item label="Title">
          <UInput v-model="form.title" placeholder="Enter the title" required />
        </UForm-item>

        <UForm-item label="Creator">
          <UInput v-model="form.creator" placeholder="Enter creator's name" required />
        </UForm-item>

        <UForm-item label="File">
          <input type="file" ref="fileInput" @change="handleFileChange" required />
        </UForm-item>

        <UButton type="primary" html-type="submit">Upload</UButton>
      </UForm>
    </UCard>
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

u-card {
  width: 400px;
  padding: 20px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

u-button {
  width: 100%;
}
</style>
