<template>
  <div class="sponsor-page">
    <section class="section animate-enter staggered">
      <h2>为什么要赞助?</h2>
      <p>支持我们让项目持续发展，帮助我们提供更好的服务。</p>
    </section>

    <section class="section animate-enter staggered">
      <h2>赞助方式</h2>
      <p class="animate-enter staggered">您可以通过扫描下方二维码赞助我</p>
      <img src="https://res.juz1.cn/img/pay.jpg" alt="JuziPay" class="JuziPay" />
      <p class="animate-enter staggered">或者访问<a href="https://pay.juz1.cn" target="_blank">pay.juz1.cn</a>赞助我</p>
    </section>

    <section class="section animate-enter staggered">
      <h2>赞助者名单</h2>
      <div v-if="sponsors.length > 0">
        <p v-for="sponsor in sponsors" :key="sponsor.id" class="sponsor-item">
          {{ sponsor.name }}: {{ sponsor.amount }}元
        </p>
      </div>
      <p v-else>暂无赞助者</p>
    </section>

    <footer class="section footer-black animate-enter">
      <p>&copy; 2023-2024 <a href="https://juz1.cn" target="_blank">Juzi</a> Made with ❤</p>
        <a href="https://beian.miit.gov.cn/" target="_blank">鄂ICP备2024068469号-1</a>
    </footer>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      sponsors: []
    };
  },
  mounted() {
    this.fetchSponsors();
    this.loadExternalScript();
  },
  methods: {
    async fetchSponsors() {
      try {
        const response = await axios.get('https://api.juz1.cn/sponsor');
        this.sponsors = response.data;
      } catch (error) {
        console.error('获取赞助者名单时出错:', error);
      }
    },
    loadExternalScript() {
      const script = document.createElement('script');
      script.src = 'https://res.juz1.cn/js/copyright.js';
      script.async = true;
      document.body.appendChild(script);
    }
  }
};
</script>

<style scoped>
@import url('https://res.juz1.cn/css/a.css');

.sponsor-page {
  text-align: center;
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

@keyframes enter {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-enter {
  animation: enter 0.3s ease both;
  animation-delay: var(--delay, 120ms);
}

.staggered:nth-child(1) {
  --delay: 0.3s;
}

.staggered:nth-child(2) {
  --delay: 0.6s;
}

.staggered:nth-child(3) {
  --delay: 0.9s;
}

.JuziPay {
  width: 200px;
  height: 200px;
  margin-top: 20px;
}

.sponsor-item {
  margin: 4px 0;
  font-size: 1rem;
}

footer.footer-black {
  background-color: white;
  color: black;
  padding: 20px;
  font-size: 0.9rem;
}


footer p {
  margin: 0;
}

footer small {
  display: block;
  margin-top: 10px;
  font-size: 0.75rem;
}
</style>
