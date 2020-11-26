<template>
  <main class="main">
    <div class="wrapper">
      <h1>Чумаков Станислав Анатольевич, 1995</h1>
      <div class="main__about">
        <div class="main__about-content">
          <div class="text">
            <h2>Опыт работы 3 года 4 месяца</h2>
            <p>За это время работал в 2х компаниях. В последней рабоатаю 2 года и 8 месяцев.</p>
            <p>Занимаю должность Тимлида</p>
          </div>
          <h2>Ключевые навыки:</h2>
          <ul class="skils">
            <li class="skils__item">HTML</li>
            <li class="skils__item">CSS</li>
            <li class="skils__item">Scss</li>
            <li class="skils__item">Gulp</li>
            <li class="skils__item">webpack</li>
            <li class="skils__item">jQuery</li>
            <li class="skils__item skils__item--new">Vue.js</li>
          </ul>

        </div>
        <div class="main__about-img">
          <img src="../assets/avatar.jpg" alt="Это я"  title="Это я">
        </div>
      </div>
    </div>
  </main>
</template>

<style lang="scss">
@keyframes float {
  0% {
    box-shadow: 0 5px 15px 0px rgba(0, 0, 0, 0.6);
    transform: translatey(0px);
  }
  50% {
    box-shadow: 0 25px 15px 0px rgba(0, 0, 0, 0.2);
    transform: translatey(-20px);
  }
  100% {
    box-shadow: 0 5px 15px 0px rgba(0, 0, 0, 0.6);
    transform: translatey(0px);
  }
}

.main {
  background-color: $black;
  padding: 64px 0;
  flex: 1 1 auto;

  &__about {
    display: flex;
    justify-content: space-between;
    align-content: flex-start;

  }

  &__about-content {
    width: calc(100% - 280px);
    padding-right: 32px;
    position: relative;
    z-index: 2;
  }

  &__about-img {
    width: 280px;
    height: 280px;
    position: relative;
    border-radius: 50%;
    background-color: $white;
    animation: float 6s ease-in-out infinite;
    overflow: hidden;

    img {
      display: block;
      width: 100%;
      height: 100%;
      object-fit: cover;
      object-position: center;
    }
  }

}

.skils {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-wrap: wrap;

  li {
    padding: 24px;
    font-size: 24px;
    line-height: 32px;
  }
}

@media (max-width: 800px){
  .main__about{
    flex-direction: column;
    align-items:center;
    justify-content: center;

    &-img {
      order: -1;
      margin-bottom: 24px;
    }
    &-content {
      width: 100%;
      padding: 0;
    }
  }


}
</style>

