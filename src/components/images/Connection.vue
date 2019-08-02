<template>
  <div class="connection" :class="position">
    <svg viewBox="0 0 100 5" xmlns="http://www.w3.org/2000/svg">
      <line x1="0" x2="100" stroke="black" />
    </svg>
  </div>
</template>

<script>
export default {
  props: ['position'],
  name: 'Connection',
};
</script>
