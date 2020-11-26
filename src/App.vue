<template>
  <div class="container" id="app">
    <div class="content">

      <header class="header">
        <div class="wrapper">
          <div class="header__logo">
            <a href="/" class="logo" data-logo="TestConstanta">TestConstanta</a>
          </div>
          <burger-menu @toggle-menu="menuActive = !menuActive" :active="menuActive"></burger-menu>
          <transition @before-enter="beforeEnter" @enter="enter" @leave="leave" :css="false">
            <Menu v-show="menuActive" :active="menuActive"></Menu>
          </transition>
        </div>
      </header>

      <router-view/>

    </div>
    <footer class="footer">
      <div class="wrapper">
        <Menu/>
        <div class="footer__right">
          <ul class="social">
            <li class="social__item">
              <a href="https://vk.com/user1011" target="_blank" rel="noopenner" class="social__link" title="Вконтакте">
                <img title="Вконтакте" alt="Вконтакте" src="./assets/vk.svg">
              </a>
            </li>
            <li class="social__item">
              <a href="https://teleg.run/spacedeveloper" target="_blank" rel="noopenner" class="social__link" title="Telegram">
                <img title="Telegram" alt="Telegram" src="./assets/telegram.svg">
              </a>
            </li>
            <li class="social__item">
              <a href="https://www.instagram.com/space_developer/" target="_blank" rel="noopenner" class="social__link" title="Instagram">
                <img title="Instagram" alt="Instagram" src="./assets/instagram.svg">
              </a>
            </li>
            <li class="social__item">
              <a href="https://github.com/zapaza" target="_blank" rel="noopenner" class="social__link" title="GitHub">
                <img title="GitHub" alt="GitHub" src="./assets/github.svg">
              </a>
            </li>
          </ul>
          <time class="date" id='date'>{{ datetime | formatDate1 }}</time>
        </div>

      </div>
    </footer>
  </div>
</template>

<script>
import Velocity from 'velocity-animate'
import Menu from '@/components/Menu.vue'
import Burger from '@/components/Burger'

export default {
  name: 'default',
  components: {
    Menu,
    'burger-menu': Burger,
  },
  data: () => ({
    datetime: new Date(),
    isMobile: window.innerWidth < 800,
    globalOverlay: {
      active: false
    },
    menuActive: window.innerWidth >= 800
  }),
  methods: {
    beforeEnter() {
      if (this.isMobile) {
        this.globalOverlay.active = true
      }
    },
    enter(el, done) {
      Velocity(el, {
        marginLeft: 0
      }, {
        complete: done
      }, {
        duration: 300
      })
    },
    leave(el, done) {
      Velocity(el, {
        complete: done
      }, {
        duration: 300
      }).then(() => {
        if (this.isMobile) {
          this.globalOverlay.active = false
        }
      })
    },
  },
  filters: {
    formatDate1: d => d.toLocaleString('ru-RU').replace(',', '').slice(0, -3),
  }
}

</script>

<style lang="scss">
@keyframes glitch {
  0% {
    transform: translate(0)
  }
  20% {
    transform: translate(-1px, 1px)
  }
  40% {
    transform: translate(-1px, -1px)
  }
  60% {
    transform: translate(1px, 1px)
  }
  80% {
    transform: translate(1px, -1px)
  }
  to {
    transform: translate(0);
  }
}

.logo {
  font-weight: $font-weight--700;
  font-size: 24px;
  line-height: 32px;
  text-decoration: none;
  text-transform: uppercase;
  color: $white;
  letter-spacing: 5px;
  position: relative;
  z-index: 2;
  display: inline-block;

  &:before, &:after {
    display: block;
    content: attr(data-logo);
    text-transform: uppercase;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    opacity: .8;
  }

  &:after {
    color: #f0f;
    z-index: -2;
  }

  &:before {
    color: #0ff;
    z-index: -1;
  }

  &:hover {
    &:before {
      animation: glitch .3s cubic-bezier(.25, .46, .45, .94) both 5
    }

    &:after {
      animation: glitch .3s cubic-bezier(.25, .46, .45, .94) reverse both 5
    }
  }
}

.header {
  border-bottom: 1px solid $white;

  .burger {
    display: none;
  }

  .menu {
    display: block;
  }
}

.header, .footer {
  width: 100%;
  padding: 16px 0;
  background-color: $black;

  .wrapper {
    display: flex;
    justify-content: space-between;
  }

  .menu {
    &__list {
      display: flex;
      list-style: none;
    }

    &__item {
      margin-right: 24px;

      &:last-child {
        margin-right: 0;
      }
    }

    &__link {
      @include transition();
      text-decoration: none;
      color: $white;
      font-size: 16px;
      line-height: 1.44;

      &:hover {
        color: $gray;
      }
    }
  }
}

.footer {
  border-top: 1px solid $white;

  .burger {
    display: none;
  }

  .social {
    display: flex;
    list-style: none;
    margin-bottom: 8px;

    &__item {
      margin-left: 24px;

      &:first-child {
        margin-left: 0;
      }
    }

    &__link {
      width: 24px;
      height: 24px;
      display: block;
      @include transition();

      img {
        display: block;
        width: 100%;
      }

      &:hover {
        filter: drop-shadow(2px 2px 2px rgba(255, 255, 255, .3));
      }

    }
  }

  .date {
    color: $white;
    display: inline-block;
  }
}

@media (max-width: 800px) {
  .footer {
    .wrapper {
      flex-direction: column;
    }

    .menu {
      margin-bottom: 16px;
    }

    .social {
      margin-bottom: 16px;
    }
  }

  .logo {
    font-size: 20px;
    line-height: 24px;
    letter-spacing: 2px;
  }
  .header {
    position: relative;
  }
  .menu {
    display: none;

    &[active=true] {
      position: absolute;
      top: 100%;
      background-color: $white;
      right: 0;

      .menu__list{
        flex-direction: column;
      }
      .menu__link {
        font-size: 16px;
        line-height: 20px;
        color: $black;
        padding: 16px;
        display: inline-block;
      }

    }
  }

}

</style>
