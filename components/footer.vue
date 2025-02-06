<template>
  <footer class="container mt-5">
    <div class="row justify-content-center">
      <div class="col-lg-10 text-center text-lg-start">
        <div class="footer-links">
          <span class="footer-item">客服專線: {{ customerService }}</span>
          <NuxtLink v-for="(link, index) in footerLinks" :key="index" :to="link.url"
            class="footer-item underline-hover">
            {{ link.text }}
          </NuxtLink>
        </div>
      </div>
      <div class="col-lg-2 text-center">
        <h4>
          <img src="/img/betting.png" class="footer-img" alt="運彩標誌" />
          運彩網
        </h4>
      </div>
    </div>
    <hr class="footer-divider" />
    <div class="footerdown text-center">
      <p>{{ footerText }}</p>
    </div>
  </footer>

  <button id="topButton" @click="scrollToTop" class="bi bi-arrow-up-circle"></button>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted, onUnmounted } from "vue";

export default defineComponent({
  name: "StaticFooter",
  setup() {
    const customerService = ref("0800-123-456");
    const footerText = ref("© 2024 運彩網平台。本網站僅用來練習，無其他用途。");
    const footerLinks = ref([
      { text: "聯絡我們", url: "#" },
      { text: "常見問題", url: "#" },
      { text: "使用條款", url: "#" },
      { text: "隱私政策", url: "#" }
    ]);

    const scrollToTop = () => {
      window.scrollTo({
        top: 0,
        behavior: "smooth"
      });
    };

    const handleScroll = () => {
      const topButton = document.getElementById("topButton");
      if (topButton) {
        topButton.style.display = window.scrollY > 100 ? "block" : "none";
      }
    };

    onMounted(() => {
      window.addEventListener("scroll", handleScroll);
    });

    onUnmounted(() => {
      window.removeEventListener("scroll", handleScroll);
    });

    return { customerService, footerText, footerLinks, scrollToTop };
  }
});
</script>

<style scoped>
.container {
  max-width: 1000px;
}

.footer-links {
  font-size: 16px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 10px;
}

.footer-item {
  color: black;
  text-decoration: none;
  position: relative;
  padding: 0 8px;
}

.footer-item:not(:first-child)::before {
  content: "|";
  position: absolute;
  left: -7px;
  color: black;
}

.underline-hover:hover {
  text-decoration: underline;
}

.footer-img {
  height: 40px;
  width: 40px;
}

.footer-divider {
  border-top: 2px solid #737475;
}

.footerdown {
  font-size: 14px;
}

#topButton {
  display: none;
  position: fixed;
  bottom: 20px;
  right: 20px;
  font-size: 50px;
  background-color: transparent;
  border: none;
}

#topButton:hover {
  color: #007bff;
}

@media (max-width: 768px) {
  .footer-links {
    font-size: 12px;
    text-align: center;
  }

  .footerdown {
    font-size: 13px;
  }
}
</style>