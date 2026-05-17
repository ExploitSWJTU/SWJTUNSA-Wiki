---
title: 关注网安谢谢喵
---

<style>
  .wiki-hero-carousel {
    position: relative;
    max-width: min(720px, 90vw);
    margin: 0 auto 1.5rem;
  }
  .wiki-hero-carousel__viewport {
    overflow: hidden;
    border-radius: 8px;
    background: var(--md-default-bg-color--lighter, #f5f5f5);
    width: 100%;
    aspect-ratio: 16 / 9;
  }
  .wiki-hero-carousel__track {
    display: flex;
    height: 100%;
    transition: transform 0.45s ease;
  }
  .wiki-hero-carousel__slide {
    flex: 0 0 100%;
    min-width: 0;
    height: 100%;
  }
  .wiki-hero-carousel__slide img {
    display: block;
    width: 100%;
    height: 100%;
    object-fit: contain;
    object-position: center;
    margin: 0;
  }
  .wiki-hero-carousel__btn {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    z-index: 2;
    width: 2.25rem;
    height: 2.25rem;
    border: none;
    border-radius: 50%;
    cursor: pointer;
    font-size: 1.5rem;
    line-height: 1;
    padding: 0;
    color: #fff;
    background: rgba(0, 0, 0, 0.35);
    transition: background 0.2s;
  }
  .wiki-hero-carousel__btn:hover {
    background: rgba(0, 0, 0, 0.55);
  }
  .wiki-hero-carousel__btn--prev {
    left: 0.35rem;
  }
  .wiki-hero-carousel__btn--next {
    right: 0.35rem;
  }
  .wiki-hero-carousel__dots {
    display: flex;
    justify-content: center;
    gap: 0.4rem;
    margin-top: 0.65rem;
  }
  .wiki-hero-carousel__dot {
    width: 0.5rem;
    height: 0.5rem;
    padding: 0;
    border: none;
    border-radius: 50%;
    cursor: pointer;
    background: rgba(0, 0, 0, 0.2);
    transition: transform 0.2s, background 0.2s;
  }
  .wiki-hero-carousel__dot[aria-selected="true"] {
    background: var(--md-typeset-a-color, #7c4dff);
    transform: scale(1.15);
  }
  [data-md-color-scheme="slate"] .wiki-hero-carousel__dot {
    background: rgba(255, 255, 255, 0.25);
  }
  [data-md-color-scheme="slate"] .wiki-hero-carousel__dot[aria-selected="true"] {
    background: var(--md-typeset-a-color, #69f0ae);
  }
</style>

<div
  class="wiki-hero-carousel"
  id="wiki-hero-carousel"
  role="region"
  aria-roledescription="carousel"
  aria-label="协会风采轮播"
>
  <div class="wiki-hero-carousel__viewport">
    <div class="wiki-hero-carousel__track" id="wiki-hero-track">
      <div class="wiki-hero-carousel__slide">
        <img src="/assets/img/logo remake.png" alt="网络安全协会logo" loading="eager" />
      </div>
      <div class="wiki-hero-carousel__slide">
        <img src="/assets/img/合照.jpg" alt="合照" loading="lazy" />
      </div>
      <div class="wiki-hero-carousel__slide">
        <img src="/assets/img/arch.jpg" alt="arch" loading="lazy" />
      </div>
      <div class="wiki-hero-carousel__slide">
        <img src="/assets/img/低客.jpg" alt="网络安全协会招新" loading="lazy" />
      </div>
      <div class="wiki-hero-carousel__slide">
        <img src="/assets/img/2026ciscn半决赛2.jpg" alt="2026 CISCN 半决赛" loading="lazy" />
      </div>
      <div class="wiki-hero-carousel__slide">
        <img src="/assets/img/pic.jpg" alt="pic" loading="lazy" />
      </div>
      <div class="wiki-hero-carousel__slide">
        <img src="/assets/img/雷神托尔.jpg" alt="雷神托尔" loading="lazy" />
      </div>
      <div class="wiki-hero-carousel__slide">
        <img src="/assets/img/新秀杯活动照片2.jpg" alt="CTF 新秀杯活动" loading="lazy" />
      </div>
      <div class="wiki-hero-carousel__slide">
        <img src="/assets/img/新秀杯活动照片.png" alt="CTF 新秀杯活动" loading="lazy" />
      </div>
      <div class="wiki-hero-carousel__slide">
        <img src="/assets/img/bcbn.png" alt="CTF NSA" loading="lazy" />
      </div>
    </div>
  </div>
  <button type="button" class="wiki-hero-carousel__btn wiki-hero-carousel__btn--prev" aria-label="上一张">‹</button>
  <button type="button" class="wiki-hero-carousel__btn wiki-hero-carousel__btn--next" aria-label="下一张">›</button>
  <div class="wiki-hero-carousel__dots" id="wiki-hero-dots" role="tablist" aria-label="选择幻灯片"></div>
</div>

<script>
  (function () {
    var root = document.getElementById("wiki-hero-carousel");
    if (!root) return;
    var track = document.getElementById("wiki-hero-track");
    var viewport = root.querySelector(".wiki-hero-carousel__viewport");
    var dotsHost = document.getElementById("wiki-hero-dots");
    var slides = track ? track.children.length : 0;
    if (slides < 2) return;

    var i = 0;
    var timer = null;
    var interval = 4000;

    function go(n) {
      i = (n + slides) % slides;
      track.style.transform = "translateX(-" + i * 100 + "%)";
      var dots = dotsHost.querySelectorAll(".wiki-hero-carousel__dot");
      for (var d = 0; d < dots.length; d++) {
        dots[d].setAttribute("aria-selected", d === i ? "true" : "false");
      }
    }

    function next() {
      go(i + 1);
    }
    function prev() {
      go(i - 1);
    }

    function armTimer() {
      clearInterval(timer);
      timer = setInterval(next, interval);
    }
    function disarmTimer() {
      clearInterval(timer);
      timer = null;
    }

    for (var s = 0; s < slides; s++) {
      (function (index) {
        var b = document.createElement("button");
        b.type = "button";
        b.className = "wiki-hero-carousel__dot";
        b.setAttribute("role", "tab");
        b.setAttribute("aria-label", "第 " + (index + 1) + " 张");
        b.addEventListener("click", function () {
          go(index);
          armTimer();
        });
        dotsHost.appendChild(b);
      })(s);
    }
    go(0);

    root.querySelector(".wiki-hero-carousel__btn--next").addEventListener("click", function () {
      next();
      armTimer();
    });
    root.querySelector(".wiki-hero-carousel__btn--prev").addEventListener("click", function () {
      prev();
      armTimer();
    });

    if (viewport) {
      viewport.addEventListener("mouseenter", disarmTimer);
      viewport.addEventListener("mouseleave", armTimer);
    }
    root.addEventListener("focusin", disarmTimer);
    root.addEventListener("focusout", function (e) {
      if (!root.contains(e.relatedTarget)) armTimer();
    });

    armTimer();
  })();
</script>

在这个信息爆炸的时代，网络世界充满了未知和挑战。你是否曾幻想自己是一名网络世界的超级英雄，守护着数字世界的和平？我们寻找的就是你——未来的网络安全卫士！ 网络安全协会，一个神秘而又充满刺激的学生组织，是每一个对网络世界充满好奇和热情的同学的秘密基地。
