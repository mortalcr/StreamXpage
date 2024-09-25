<template>
  <div class="upload-container">
    <UCard>
      <UForm @submit="handleSubmit">
        <UForm-item label="Title">
          <UInput v-model="form.title" placeholder="Enter the title" required />
        </UForm-item>

        <UForm-item label="Creator">
          <UInput v-model="form.creator" placeholder="Enter creator's name" required />
        </UForm-item>

        <UForm-item label="File">
          <UInput type="file" v-model="form.media" accept="*/*" required />
        </UForm-item>

        <UButton type="primary" html-type="submit">Upload</UButton>
      </UForm>
    </UCard>
  </div>
</template>

<script>
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
    handleSubmit() {
      const formData = new FormData();
      formData.append('title', this.form.title);
      formData.append('creator', this.form.creator);
      formData.append('media', this.form.media);

      // Aquí envías el formData a tu backend
      fetch('http://localhost:8080/api/upload', {
        method: 'POST',
        body: formData
      })
        .then(response => response.json())
        .then(data => console.log(data))
        .catch(error => console.error('Error:', error));
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
