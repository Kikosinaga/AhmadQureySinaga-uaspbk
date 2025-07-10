<template>
  <div :class="['alert', type]">
    <span>{{ message }}</span>
    <button class="close-btn" @click="$emit('close')">&times;</button>
  </div>
</template>

<script setup>
defineProps({ type: String, message: String })
</script>

<style scoped>
.alert {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1rem 1.5rem;
  border-radius: 8px;
  margin: 1rem 0;
  font-weight: bold;
  font-size: 1rem;
  box-shadow: 0 2px 8px rgba(0,0,0,0.08); /* Bayangan tetap, opacity disesuaikan */
}

/* Alert SUKSES */
.alert.success {
  background: #ffc9db; /* Pink sangat muda untuk sukses */
  color: #880E4F; /* Deep Pink untuk teks sukses */
}

/* Alert INFO */
.alert.info {
  background: #F48FB1; /* Pink medium untuk info */
  color: white; /* Teks putih untuk info */
}

/* Alert WARNING */
.alert.warning {
  background: #EC407A; /* Pink aksen/kuat untuk warning */
  color: white; /* Teks putih untuk warning */
}

.close-btn {
  background: none;
  border: none;
  color: inherit; /* Akan mewarisi warna teks dari .alert.type */
  font-size: 1.5rem;
  cursor: pointer;
  margin-left: 1rem;
}

/* Tambahan: efek hover untuk tombol close agar lebih interaktif */
.close-btn:hover {
  opacity: 0.7;
}
</style>
