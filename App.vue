<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'; // ref をインポート

// 動画リストを定義
const videoSources = [
  "/assets/214409_tiny.mp4",
  "/assets/246856_tiny.mp4",
  "/assets/253423_small.mp4",
];

// 現在の動画インデックスを管理
const currentVideoIndex = ref(0);
const isFading = ref(false); // フェードアニメーションの状態を管理
// 動画の切り替えロジック
let intervalId: number | undefined;

const changeVideo = () => {
  isFading.value = true; // フェードアウト開始
  setTimeout(() => {
    currentVideoIndex.value =
      (currentVideoIndex.value + 1) % videoSources.length; // 次の動画に切り替え
    isFading.value = false; // フェードイン開始
  }, 1000); // フェードアウトの時間（1秒）
};

// コンポーネントがマウントされたときにタイマーを開始
onMounted(() => {
  intervalId = setInterval(changeVideo, 10000); // 10秒ごとに切り替え
});

// コンポーネントがアンマウントされたときにタイマーをクリア
onUnmounted(() => {
  if (intervalId) clearInterval(intervalId);
});
</script>


<template>
  <body>
    <header class="header">
      <h1 class="headline">
        <a href="./index/">vue.js practice</a>
      </h1>
      <nav>
        <ul class="nav-list">
          <li class="nav-list-item"><a href="./index/">Home</a></li>
          <li class="nav-list-item">
            <a href="#about">About</a>
          </li>
          <li class="nav-list-item">
            <a href="#contact">Contact</a>
          </li>
        </ul>
      </nav>
    </header>

    <main>
      <section class="hero">
        <video autoplay loop muted preload="auto" :src="videoSources[currentVideoIndex]"
        :class="{ fade: isFading }">
        </video>
        <strong class="hero-text">
          vue.js
        </strong>
      </section>

      <section class="about" id="about">
        <h1 class="about-headline">About</h1>
        <div class="about-div">
          <img src="./assets/art1.png" alt="img" class="about-image" />
          <p class="about-paragraph">text text text text text text text text text text text text text text </p>
        </div>
      </section>

      <section class="contact" id="contact">
        <h1 class="contact-headline">Contact</h1>
        <table class="contact-table">
          <tr class="contact-table-row">
            <th>名前</th>
            <td><input type="text" /></td>
          </tr>
          <tr class="contact-table-row">
            <th>メールアドレス</th>
            <td><input type="email" /></td>
          </tr>
          <tr class="contact-table-row">
            <th>電話番号</th>
            <td><input type="tel" /></td>
          </tr>
          <tr class="contact-table-row">
            <th>年齢</th>
            <td>
              <select name="" id="">
                <option value="">選択してください</option>
                <option value="1">10代</option>
                <option value="2">20代</option>
                <option value="3">30代</option>
                <option value="4">40代</option>
                <option value="5">50代</option>
                <option value="6">60代以上</option>
              </select>
            </td>
          </tr>
          <tr class="contact-table-row">
            <th>check box</th>
            <td class="checkbox">
              <input type="checkbox" name="1" id="check1" />
              <label for="check1">1</label>
              <input type="checkbox" name="2" id="check2" />
              <label for="check2">2</label>
              <input type="checkbox" name="3" id="check3" />
              <label for="check3">3</label>
            </td>
          </tr>
          <tr class="contact-table-row">
            <th>メッセージ</th>
            <td><textarea></textarea></td>
          </tr>
          <tr class="contact-table-row">
            <td colspan="2">
              <button type="submit">送信</button>
            </td>
          </tr>
        </table>
      </section>

      <footer class="footer">
        <p class="footer-paragraph">© 2023 vue.js practice</p>
      </footer>
    </main>
  </body>
</template>

<style scoped>
body {
  font-family: "NotoSerifJP-Light", serif, "Helvetica Neue", "Helvetica",
    "Hiragino Sans", "Hiragino Kaku Gothic ProN", "Arial", "Yu Gothic", "Meiryo",
    sans-serif;
  font-optical-sizing: auto;
  font-weight: weight;
  font-style: normal;
  background: linear-gradient(to bottom, #0008ff, #333);
  color: white;
  overflow: hidden;
  scroll-behavior: smooth;
}

/* header */
.header {
  background-color: #333;
  color: white;
  padding: 0 0 0 20px;
  display: flex;
  justify-content: space-between;
  position:fixed;
  top: 0;
  left: 0;
  width:100%;
  z-index: 1000;
}

.headline {
  font-size: 2em;
  margin: 0;
}
.headline a {
  color: white;
  text-decoration: none;
}n

.nav-list {
  list-style-type: none;
  padding: 0;
}

.nav-list-item {
  display: inline-block;
  padding: 0 10px;
  margin-right: 60px;
  color: white;
  text-decoration: none;
  transition: background-color 0.2s ease;
}
.nav-list-item a {
  color: white;
  text-decoration: none;
}

.nav-list-item:hover {
  background-color: #686868;
}

/* hero */
.hero {
  position: relative;
  width: 100%;
  height: 100vh;
  overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
}

.hero video {
  position:absolute;
  width: 100%;
  height: auto;
  display: block;
  transition: opacity 1s ease; /* フェードアニメーションの時間 */
  opacity: 1;
  overflow: hidden;
  z-index: 0; /* 背景に配置 */
  object-fit:cover;
  
}

video.fade {
  opacity: 0; /* フェードアウト時の透明度 */
  
}

.hero-text {
  position: absolute;
  color: rgb(160, 255, 199);
  font-size: 5em;
  text-align: center;
  z-index: 1; /* テキストを前面に配置 */
}

.about {
  padding: 20px;
  text-align: center;
}
.about-headline {
  font-size: 3em;
  margin: 20px 0;
}
.about-div {
  display: flex;
  align-items: center;
  justify-content: center;
}
.about-image {
  width: 100%;
  max-width: 600px;
  height: auto;
  margin-right: 30px;
}
.about-paragraph {
  margin: 20px ;
}

/* contact */
.contact {
  padding: 20px;
  text-align: center;
}
.contact-headline {
  font-size: 3em;
  margin: 20px 0;
}
.contact-table {
  margin: 0 auto;
  width: 80%;
  max-width: 600px;
  border-collapse: collapse;
}
.contact-table-row {
  border-bottom: 1px solid #ccc;
}
.contact-table-row th {
  text-align: left;
  padding: 10px;
}
.contact-table-row td {
  padding: 10px;
}
.contact-table-row input,
.contact-table-row select,
.contact-table-row textarea {
  width: 100%;
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 4px;
}
.checkbox {
  display: flex;
  justify-content: center;
  align-items: center;
}
.contact-table-row button {
  background-color: #333;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
.contact-table-row button:hover {
  background-color: #686868;
}
.contact-table-row label {
  margin-right: 10px;
}
.contact-table-row input[type="checkbox"] {
  margin-right: 5px;
}
.contact-table-row input[type="checkbox"] + label {
  margin-right: 20px;
}
.contact-table-row textarea {
  height: 100px;
}
.contact-table-row select option {
  padding: 5px;
}
.contact-table-row select option:hover {
  background-color: #333;
  color: white;
}
.contact-table-row select option:active {
  background-color: #686868;
  color: white;
}
.contact-table-row select option:focus {
  outline: none;
  box-shadow: 0 0 5px #333;
}
.contact-table-row select option:focus-visible {
  outline: none;
  box-shadow: 0 0 5px #333;
}

/* footer */
.footer {
  text-align: center;
  width: 100%;
  border-top:#fff 1px solid;
  padding: 0;
  margin: 0;
}

/* responsive */
@media (max-width: 768px) {
  .header {
    align-items: center;
  }
  .headline {
    font-size: 1em;
  }
  .nav-list-item {
    margin-right: 0px;
  }
  .hero {
    height: 100vh;
  }
  .hero video {
    width: auto;
    height: 100vh;
  }
  .hero-text {
    font-size: 3em;
  }
  .about-image {
    width: 50%;
    height: auto;
    margin-right: 0;
  }
  .about-paragraph {
    margin: 10px;
  }
}
</style>
