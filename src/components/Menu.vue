<template>
    <nav class="menu"  >
        <ul class="menu__list" id="nav">
            <li class="menu__item"><router-link class='menu__link' to="/">Главная</router-link></li>
            <li class="menu__item"><router-link class='menu__link' to="/contacts">Контакты</router-link></li>
        </ul>
    </nav>

</template>

<script>
export default {
  name: 'Menu',
}
</script>
