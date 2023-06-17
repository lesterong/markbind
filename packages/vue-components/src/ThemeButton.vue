<template>
  <button
    :class="['theme-button']"
    type="button"
    @click="toggleTheme()"
  >
    <i v-if="theme === 'dark'" :class="['fas fa-moon']"></i>
    <i v-else :class="['fas fa-sun']"></i>
  </button>
</template>

<script>
export default {
  name: 'ThemeButton',
  data() {
    return {
      theme: 'light',
    };
  },
  methods: {
    initThemeButton() {
      const hasInitTheme = localStorage.getItem('theme') && (
        localStorage.getItem('theme') === 'light' || localStorage.getItem('theme') === 'dark'
      );
      if (!hasInitTheme) {
        if (window.matchMedia('(prefers-color-scheme: dark)').matches) {
          localStorage.setItem('theme', 'dark');
        } else {
          localStorage.setItem('theme', 'light');
        }
      }
      this.theme = localStorage.getItem('theme');
      document.documentElement.setAttribute('data-theme', this.theme);
    },
    toggleTheme() {
      if (this.theme === 'light') {
        this.theme = 'dark';
      } else {
        this.theme = 'light';
      }
      localStorage.setItem('theme', this.theme);
      document.documentElement.setAttribute('data-theme', this.theme);
    },
  },
  mounted() {
    this.initThemeButton();
  },
};
</script>

<style scoped>
    .theme-button {
        background-color: transparent;
        border: 0;
    }
</style>
