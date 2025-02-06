<template>
  <nav class="navbar navbar fixed-top bg-body-secondary shadow-sm">
    <div class="container">
      <div class="navbar">
        <form class="d-flex">
          <button class="btn btn-sm btn-outline-secondary login-btn" type="button">
            <i class="bi bi-lock"></i>{{ loginText }}
          </button>
          <button class="btn btn-sm btn-outline-secondary signup-btn" type="button">
            <i class="bi bi-person"></i>{{ signupText }}
          </button>
        </form>
      </div>
    </div>
  </nav>

  <nav class="navbar navbar-expand-lg navbar-light bg-light navbar-custom">
    <div class="container">
      <NuxtLink to="/" class="navbar-brand">
        <img :src="logoSrc" style="height: 50px; width: 50px;" />{{ siteName }}
      </NuxtLink>
      <button class="navbar-toggler navbar-dark" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav"
        aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse justify-content-end" id="navbarNav">
        <ul class="navbar-nav">
          <li v-for="(menu, index) in navItems" :key="index" class="nav-item dropdown">
            <a class="nav-link dropdown-toggle" href="#" data-bs-toggle="dropdown">{{ menu.title }}</a>
            <ul class="dropdown-menu">
              <li v-for="(sub, subIndex) in menu.submenu" :key="subIndex">
                <NuxtLink class="dropdown-item" :to="sub.link">{{
                  sub.text
                }}</NuxtLink>
              </li>
            </ul>
          </li>
        </ul>
      </div>
    </div>
  </nav>

  <div id="news-carousel" class="carousel slide" data-bs-ride="carousel">
    <div class="carousel-inner">
      <div v-for="(news, index) in newsItems" :key="index" class="carousel-item" :class="{ active: index === 0 }">
        <h3>{{ news }}</h3>
      </div>
    </div>
    <button class="carousel-control-prev" type="button" data-bs-target="#news-carousel" data-bs-slide="prev">
      <span class="carousel-control-prev-icon" aria-hidden="true"></span>
      <span class="visually-hidden"></span>
    </button>
    <button class="carousel-control-next" type="button" data-bs-target="#news-carousel" data-bs-slide="next">
      <span class="carousel-control-next-icon" aria-hidden="true"></span>
      <span class="visually-hidden"></span>
    </button>
  </div>
</template>

<script lang="ts">
import { defineComponent, type PropType } from "vue";

export default defineComponent({
  name: "Navbar",
  props: {
    loginText: {
      type: String,
      default: "登入",
    },
    signupText: {
      type: String,
      default: "加入會員",
    },
    logoSrc: {
      type: String,
      default: "img/betting.png",
    },
    siteName: {
      type: String,
      default: "運彩網",
    },
    navItems: {
      type: Array as PropType<
        {
          title: string;
          submenu: { text: string; link: string }[];
        }[]
      >,
      default: () => [
        { title: "玩競猜", submenu: [{ text: "遊戲區", link: "#" }] },
        {
          title: "預測賽事",
          submenu: [
            { text: "預測賽事", link: "/predictgame" },
            { text: "觀看預測比分", link: "#" },
          ],
        },
        { title: "討論區", submenu: [{ text: "運彩版", link: "/forum" }] },
        {
          title: "找高手",
          submenu: [
            { text: "莊家殺手", link: "#" },
            { text: "單場殺手", link: "#" },
            { text: "勝率榜", link: "#" },
            { text: "主推榜", link: "#" },
          ],
        },
        {
          title: "即時比分",
          submenu: [
            { text: "經典版", link: "#" },
            { text: "手機版", link: "#" },
          ],
        },
        {
          title: "看數據",
          submenu: [
            { text: "對戰資訊", link: "#" },
            { text: "球隊資訊", link: "#" },
            { text: "戰績排名", link: "#" },
            { text: "賽事結果查詢", link: "#" },
          ],
        },
        { title: "玩家搜尋", submenu: [{ text: "熱門玩家", link: "#" }] },
      ],
    },
    newsItems: {
      type: Array as PropType<string[]>,
      default: () => [
        "籃球賽事分析：近期勝率排行",
        "棒球聯賽趨勢：熱門球隊表現解析",
        "即時賠率變化，掌握最佳投注時機",
      ],
    },
  },
});
</script>


<style scoped>
.navbar {
  display: flex;
  justify-content: flex-end;
  width: 100%;
}

.navbar-custom {
  background: linear-gradient(90deg, #1192e2, #36bfde);
  box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
  margin-top: 60px;
}

.container {
  max-width: 1000px;
}


.navbar-brand {
  text-align: left;
  align-content: end;
  color: white;
  font-size: 2rem;
}

.navbar-toggler {
  border: none;
}

.nav-link {
  color: white !important;
  font-size: 16px;
  text-align: center;
}

.dropdown-menu {
  background-color: #ffffff;
  border-radius: 10px;
  padding: 10px 0;
  box-shadow: 0px 6px 12px rgba(0, 0, 0, 0.15);
  animation: fadeIn 0.3s ease-out;
}

.dropdown-menu .dropdown-item {
  font-size: 14px;
  padding: 10px 0px;
  color: #333;
  text-align: center;
  transition: background-color 0.3s ease, color 0.3s ease;
}

.dropdown-menu .dropdown-item:hover {
  background-color: #24d8f4;
  color: white;
}

.dropdown-shadow {
  animation: fadeIn 0.3s ease-out;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.login-btn,
.signup-btn,
button {
  border: none;
  background-color: transparent;

}

.login-btn:hover,
.signup-btn:hover,
button:hover {
  background-color: initial;
  color: #000;
  transform: scale(1.1);
}

.carousel-item {
  text-align: center;
}

#news-carousel {
  background-color: #d4e3f3;
  padding: 1px;
  box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.1);
}

.carousel-item h3 {
  background-color: #f8f9fa;
  padding: 1px 70px;
  border-radius: 20px;
  display: inline-block;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.2);
  color: #343a40;
  margin: 10px;
  cursor: pointer;
}

@media (max-width: 768px) {
  .carousel-item h3 {
    padding: 1px 10px;
    font-size: 18px;

  }
}

@media (max-width: 768px) {
  .carousel-item h3 {
    padding: 1px 10px;
    font-size: 14px;
    border-radius: 10px;
  }
}
</style>