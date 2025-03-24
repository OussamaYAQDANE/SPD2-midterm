<script setup>

</script>

<template>
  <div class="card">
    <div class="card-image">
      <slot name="image"></slot>
    </div>
    <div class="card-content">
      <div class="card-title">
        <slot name="title"></slot>
      </div>
      <div class="card-description">
        <slot name="description"></slot>
      </div>
    </div>
    <div class="card-actions">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.card {
  background-color: white;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
  overflow: hidden;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
  width: 100%;
  
  margin: 2px;
}

.card:hover {
  transform: translateY(-5px);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
}

.card-image img {
  width: 100%;
  height: 200px;
  object-fit: cover;
  border-top-left-radius: 8px;
  border-top-right-radius: 8px;
}

.card-content {
  padding: 20px;
}

.card-title {
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 10px;
}

.card-description {
  font-size: 1rem;
  color: #333;
}

.card-actions {
  border-top: 1px solid #eee;
  padding: 10px;
  display: flex;
  justify-content: flex-end;
}

.card-actions button {
  padding: 8px 16px;
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin-left: 10px;
}

.card-actions button:hover {
  background-color: #218838;
}
</style>