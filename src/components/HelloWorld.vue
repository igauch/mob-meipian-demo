<template>
  <div>
    <div id="nav" class="nav-swiper">
      <swiper :options="navSwiperOptions">
        <swiper-slide>热点</swiper-slide>
        <swiper-slide>关注</swiper-slide>
        <swiper-slide>身边</swiper-slide>
        <div class="bar" id="nav-bar">
          <div class="bar-line"></div>
        </div>
      </swiper>
    </div>
    <div id="page">
      <swiper :options="pageSwiperOptions">
        <swiper-slide>
          <div class="carousel-swiper">
            <swiper :options="carouselOptions">
              <swiper-slide>
                <a target="_blank" href="http://www.meipian.cn/155zvbgr">
                  <img class="carousel-swiper-img" src="https://ss2.meipian.me/config/1520528285003.jpg"/>
                </a>
              </swiper-slide>
              <swiper-slide>
                <a target="_blank" href="http://www.meipian.cn/14vvxr9n">
                  <img class="carousel-swiper-img" src="https://ss2.meipian.me/config/1520237005736.jpg"/>
                </a>
              </swiper-slide>
              <swiper-slide>
                <a target="_blank" href="http://www.meipian.cn/151ackbw">
                  <img class="carousel-swiper-img" src="https://ss2.meipian.me/config/1520561628527.jpg"/>
                </a>
              </swiper-slide>
              <div class="swiper-pagination" slot="pagination"></div>
            </swiper>
          </div>

          <div class="main">
            <div class="item" v-for="item in list" v-cloak>
              <p class="info">
                <a class="author" target="_blank" :href="'https://www.meipian.cn/c/' + item.author_id ">
                  <img :src="item.author_head" class="bg">
                  <em class="oneline">{{ item.author }}</em>
                </a>
              </p>
              <div class="summary">
                <a class="title" target="_blank" :href=" 'https://' + item.domain + '/' + item.article_id">
                  {{item.title }}
                </a>
              </div>
              <a class="img-main" target="_blank" :href=" 'https://' + item.domain + '/' + item.article_id">
                <div class="bg img" :style="{ backgroundImage: 'url(' + item.cover_img_url + ')' }"></div>
              </a>
              <comment :item="item"/>
            </div>
          </div>

          <div id="wait" v-show="loading">
            <div class="loading-warp">
              <div class="loading"></div>
            </div>
          </div>
        </swiper-slide>
        <swiper-slide>对编程我总是谦卑的，对工作我总是务实的
          <br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>谢谢
          <br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>Thank you very much!
        </swiper-slide>
        <swiper-slide>策略或技巧的失误（确切来说我是耿直着去的😂）希望能不影响你对我的看法
          <br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>谢谢
          <br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>Thank you very much!
        </swiper-slide>
      </swiper>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';
  import _ from 'lodash';
  import comment from './comment';

  let navSwiperConstructor = '';
  let pageSwiperConstructor = '';
  const navSwiperInitCallback = function () {
    navSwiperConstructor = this;
  };
  const pageSwiperInitCallback = function () {
    pageSwiperConstructor = this;
  };
  const navSwiperClickCallback = function () {
    pageSwiperConstructor.slideTo(this.clickedIndex);
  };
  const navSwitchTransition = function () {
    const $navBar = document.getElementById('nav-bar');
    navSwiperConstructor.slides[pageSwiperConstructor.previousIndex].style.color = '#333';
    navSwiperConstructor.slides[pageSwiperConstructor.activeIndex].style.color = '#2887f0';
    $navBar.style.left = pageSwiperConstructor.activeIndex * 33.3333 + '%';
  };
  const pageSwiperSlideChangeCallback = function () {
    navSwiperConstructor.slideTo(this.activeIndex);
    navSwitchTransition();
  };

  export default {
    name: 'HelloWorld',
    components: {
      comment
    },
    data() {
      return {
        navSwiperOptions: {
          slidesPerView: 3,
          on: {
            init: navSwiperInitCallback,
            click: navSwiperClickCallback
          }
        },
        pageSwiperOptions: {
          watchSlidesProgress: true,
          resistanceRatio: 0,
          autoHeight: true,
          on: {
            init: pageSwiperInitCallback,
            slideChange: pageSwiperSlideChangeCallback
          }
        },
        carouselOptions: {
          pagination: {
            el: '.swiper-pagination',
            clickable: true,
          },
          loop: true,
          autoplay: {
            delay: 2500,
            disableOnInteraction: false
          }
        },
        list: [],
        loading: true
      }
    },
    methods: {
      getArticleList(max_id = "248768") {
        this.loading = true;
        axios.post('/php/default/article.php', {
          category_id: "10",
          max_id: max_id,
          controller: "category",
          action: "list"
        }).then(res => {
          this.list = this.list.concat(res.data.articles);
          this.loading = false;
        })
      }
    },
    created() {
      this.getArticleList();
      window.addEventListener('scroll', _.throttle(() => {
        if (window.pageYOffset>200 && ( window.pageYOffset + window.innerHeight > document.documentElement.scrollHeight - 100) ) {
          this.getArticleList(this.list[this.list.length - 1].id);
        }
      }, 200));
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
  $primary: #2887f0;
  .nav-swiper {
    font-size: 1.15rem;
    position: fixed;
    top: 0;
    width: 100%;
    z-index: 9999;
    background-color: #fff;
    user-select: none;
    &:after {
      content: '';
      height: 1px;
      width: 100%;
      font-size: 0;
      line-height: 0;
      background-color: #dedede;
      display: block;
    }
    .swiper-container {
      margin: 0 auto;
      line-height: 2;
      max-width: 280px;
      overflow: visible;
    }
    .swiper-wrapper {
      position: relative;
    }
    .swiper-slide {
      text-align: center;
      color: #333;
      transition: all 300ms;
      &:nth-child(1) {
        color: $primary;
      }
    }
    .bar {
      position: absolute;
      bottom: -1px;
      line-height: 0;
      width: 33.3333%;
      left: 0;
      transition: all 300ms;
      .bar-line {
        margin: 0 auto;
        height: 2px;
        width: 2.5rem;
        background-color: $primary;
      }
    }
  }

  #page {
    margin-top: 39px;
  }

  .carousel-swiper {
    .carousel-swiper-img {
      width: 100%;
    }
    .swiper-pagination-bullet-active {
      background: #dfdfdc;
    }
  }

  .main {
    background-color: #f3f3f3;
  }

  .item {
    width: 100%;
    margin-bottom: 6px;
    background-color: #fff;
    .img-main .img {
      width: 100%;
      height: 260px;
    }
    .info, .summary, .comment {
      margin: 0 16px;
      padding: 10px 0;
    }
    .info {
      line-height: 0;
      .author {
        color: #555;
      }
      img {
        width: 2rem;
        height: 2rem;
        border-radius: 50%;
        margin-right: 6px;
      }
      em {
        line-height: 2rem;
        position: absolute;
      }
    }
    .summary {
      padding-top: 0;
      .title {
        color: #333;
        font-size: 1.15rem;
      }
    }
    .bg {
      background-repeat: no-repeat;
      background-size: cover;
      background-position: 50%;
    }
  }

  #wait {
    margin: 50px 0 10px;
    .loading-warp {
      width: 30px;
      height: 30px;
      box-sizing: border-box;
      position: relative;
      margin: 20px auto 10px;
    }
    @keyframes loading-animate-before {
      0% {
        -webkit-transform: translate(-5px, -5px);
        transform: translate(-5px, -5px)
      }
      50% {
        -webkit-transform: translate(0);
        transform: translate(0)
      }
      to {
        -webkit-transform: translate(-5px, -5px);
        transform: translate(-5px, -5px)
      }
    }
    @keyframes loading-animate-after {
      0% {
        -webkit-transform: translate(5px, 5px);
        transform: translate(5px, 5px)
      }
      50% {
        -webkit-transform: translate(0);
        transform: translate(0)
      }
      to {
        -webkit-transform: translate(5px, 5px);
        transform: translate(5px, 5px)
      }
    }
    .loading {
      animation: loading-animate 1s linear infinite;
      &:before {
        border-radius: 50%;
        content: "";
        width: 15px;
        height: 15px;
        display: block;
        box-sizing: border-box;
        background-color: $primary;
        position: absolute;
        top: 0;
        left: 0;
        animation: loading-animate-before 1s ease-in-out infinite;
      }
      &:after {
        bottom: 0;
        right: 0;
        animation: loading-animate-after 1s ease-in-out infinite;
        border-radius: 50%;
        content: "";
        width: 15px;
        height: 15px;
        display: block;
        box-sizing: border-box;
        background-color: $primary;
        position: absolute;
      }
    }
  }
</style>
