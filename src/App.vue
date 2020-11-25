<template>
<div class="container" id="app">
  <div class="content" >

    <header class="header">
      <div class="wrapper">
        <Menu/>
      </div>
    </header>

    <router-view/>

  </div>
  <footer class="footer">
      <div class="wrapper"> 
          <Menu/>
          <ul class="social">
            <li class="social__item">
                <a href="" target="_blank" rel="noopenner" class="social__link" title="Вконтакте"></a>
            </li>
            <li class="social__item">
                <a href="" target="_blank" rel="noopenner" class="social__link" title="Telegram"></a>
            </li>
            <li class="social__item">
                <a href="" target="_blank" rel="noopenner" class="social__link" title="Instagram"></a>
            </li>
          </ul>
        </div>
    </footer>
  </div>
</template>

<script>
import Menu from '@/components/Menu.vue'
  export default {
  name: 'default',
  components: {
    Menu
  }
}
</script>

<style  lang="scss">
.header, .footer{
  width: 100%;
  padding: 16px 0;
  background-color: $black;

  .menu {
    &__list {
      display: flex;
      list-style:none;
    }
    &__item {
      margin-right: 24px;
      &:last-child{
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
  .wrapper {
    display: flex;
    justify-content: space-between;
  }
  .social {
    display: flex;
    list-style: none;

    &__item {
      margin-left: 24px;
      &:first-child{
        margin-left: 0;
      }
    }
    &__link {
      width: 24px;
      height: 24px;
      display: block;
      border: 1px solid $gray
    }
  }
}

</style>
