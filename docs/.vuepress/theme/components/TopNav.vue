<template>
  <div class="top-nav">
    <div class="nav-text">
      {{ displayText }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'TopNav',

  data() {
    return {
      displayText: '',
    };
  },

  mounted() {
    this.changeText();

    this.$router.afterEach(() => {
      this.isSidebarOpen = false;
      this.changeText();
    });
  },

  methods: {
    changeText() {
      let currentPath = this.$route.path.split('/');
      let version = currentPath[1];

      if (['2.x'].includes(version)) {
        this.displayText =  'This is the documentation for the current version (v2.0) of Bagisto. Stay informed and make the most of Bagisto\'s capabilities.';
      } else {
        this.displayText = 'Heads up: You are viewing outdated documentation for Bagisto. Please consider upgrading to v2.0 for the latest information.';
      }
    },
  },

}
</script>

<style>
  .top-nav {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: rgb(255, 164, 35);
    color: #fff;
    padding: 0.5rem;
    z-index: 20;
  }

  .nav-text {
    color: #0e0d0d;
    text-align: center;
    margin: 0 auto;
    font: bold;
  }

  /* Responsive Styles */
  @media (max-width: 500px) {
    .top-nav {
      flex-direction: column;
      align-items: flex-start;
    }
    .nav-text {
      margin-right: 0;
      margin-bottom: 0.5rem;
    }
  }
</style>
