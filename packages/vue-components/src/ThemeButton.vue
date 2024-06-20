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
      const hasInitTheme = localStorage.theme && (
        localStorage.theme === 'light' || localStorage.theme === 'dark'
      );
      if (!hasInitTheme) {
        if (window.matchMedia('(prefers-color-scheme: dark)').matches) {
          this.theme = 'dark';
        } else {
          this.theme = 'light';
        }
      } else {
        this.theme = localStorage.theme;
      }
      if (this.theme === 'dark') {
        this.setDarkTheme();
      } else {
        this.setLightTheme();
      }
    },
    setDarkTheme() {
      localStorage.theme = 'dark';
      const codeblockLight = document.querySelector('[href="/markbind/css/codeblock-light.min.css"]');
      if (codeblockLight) {
        codeblockLight.setAttribute('href', '/markbind/css/codeblock-dark.min.css');
      }
      document.documentElement.setAttribute('data-theme', 'dark');
    },
    setLightTheme() {
      localStorage.theme = 'light';
      const codeblockDark = document.querySelector('[href="/markbind/css/codeblock-dark.min.css"]');
      if (codeblockDark) {
        codeblockDark.setAttribute('href', '/markbind/css/codeblock-light.min.css');
      }
      document.documentElement.setAttribute('data-theme', 'light');
    },
    toggleTheme() {
      if (this.theme === 'light') {
        this.theme = 'dark';
        this.setDarkTheme();
      } else {
        this.theme = 'light';
        this.setLightTheme();
      }
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
