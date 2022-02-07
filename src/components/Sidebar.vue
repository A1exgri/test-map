<template>
  <div class="sidebar">
      <h3>Личный кабинет</h3>
      <ul>
        <li v-for="(m, index) in menu"
            :key="index"
            @click="dropdown($event)">
          <router-link :to="m.link" :class="m.items ? 'dropdown' : ''" :data-index="index">

            <span class="img-container">
              <img class="icon" :src="m.logo" :alt="m.title" />
            </span>
            {{ m.title }}
            <span v-if="m.items && (activeItem == index)" class="img-container" :id="`arrow-top-${index}`">
              <img class="icon ml-3" src="/img/project-icons/arrow-top.svg" />
            </span>
            <span v-if="m.items && activeItem != index" class="img-container" :id="`arrow-down-${index}`">
              <img class="icon ml-3" src="/img/project-icons/arrow-down.svg" />
            </span>
          </router-link>
          <ul v-if="m.items" class="dropdown-items" :id="`dropdown-items-${index}`">
            <li v-for="(item, index) in m.items" :key="index" class="dropdown-item">
              <router-link :to="item.link">
              <span class="img-container">
                <img class="icon" :src="item.logo" :alt="item.title" />
              </span>
                {{ item.title }}
              </router-link>
            </li>
          </ul>
        </li>
      </ul>
  </div>
</template>

<script>
export default {
  name: 'Sidebar',
  props: {
    msg: String
  },
  data() {
    return {
      menu: [
        {title: 'Дашбоард', link: '/', logo: '/img/project-icons/dashboard.svg'},
        {title: 'Ситуационный центр', link: '/', logo: '/img/project-icons/sit_center.svg'},
        {title: 'Активный гражданин ', link: '/', logo: '/img/project-icons/hand.svg'},
        {title: 'Службы города', link: '/', logo: '/img/project-icons/service.svg', items: [
            {title: 'Служба 1', link: '/', logo: '/img/project-icons/service.svg'},
            {title: 'Служба 2', link: '/', logo: '/img/project-icons/service.svg'},
            {title: 'Служба 3', link: '/', logo: '/img/project-icons/service.svg'},
          ]},
        {title: 'Бизнес', link: '/', logo: '/img/project-icons/business.svg', items: [
            {title: 'Бизнес 1', link: '/', logo: '/img/project-icons/business.svg'},
            {title: 'Бизнес 2', link: '/', logo: '/img/project-icons/business.svg'},
          ]},
        {title: 'Платные услуги', link: '/', logo: '/img/project-icons/pay.svg', items: [
            {title: 'Платная услуга 1', link: '/', logo: '/img/project-icons/pay.svg'},
            {title: 'Платная услуга 1', link: '/', logo: '/img/project-icons/pay.svg'},
          ]},
        {title: 'Безопасность', link: '/', logo: '/img/project-icons/safety.svg', items: [
            {title: 'Безопасность 1', link: '/', logo: '/img/project-icons/safety.svg'},
            {title: 'Безопасность 2', link: '/', logo: '/img/project-icons/safety.svg'},
          ]},
        {title: 'Инфраструктура', link: '/', logo: '/img/project-icons/infrastructure.svg', items: [
            {title: 'ГИС ЖКХ', link: '/', logo: '/img/project-icons/gis.svg'},
            {title: 'АСУДД', link: '/', logo: '/img/project-icons/asudd.svg'},
            {title: 'Электропитание', link: '/', logo: '/img/project-icons/electro.svg'},
            {title: 'БС сотовой связи', link: '/', logo: '/img/project-icons/bs.svg'},
            {title: 'Мусор', link: '/', logo: '/img/project-icons/trash.svg'},
            {title: 'Счетчики', link: '/', logo: '/img/project-icons/counter.svg'},
            {title: 'Диспетчер лифтов', link: '/', logo: '/img/project-icons/lift.svg'}
          ]},
      ],
      activeItem: '',
      isActive: false
    }
  },
  methods: {
    dropdown(e) {
      if (e.target.classList.contains('dropdown')) {
          document.querySelectorAll('.dropdown-items').forEach(i => i.classList.remove('show'))
          document.getElementById(`dropdown-items-${e.target.dataset.index}`).classList.toggle('show')
        this.activeItem = e.target.dataset.index
      }
    }
  }
}
</script>

<style scoped lang="scss">
.sidebar {
  background: #091F52;
  width: 284px;
  height: 100Vh;
  padding: 40px 0;

  h3 {
    font-weight: 800;
    font-size: 20px;
    line-height: 24px;
    color: #fff;
    padding: 0 10px 32px 40px;
  }

  ul {
    list-style-type: none;
    padding: 0;
    margin: 0;

    a {
      padding: 12px 10px 12px 40px;
      display: block;
      color: #fff;
      font-weight: 500;
      font-size: 16px;
      line-height: 20px;
      text-decoration: none;
      opacity: .72;

      &:hover {
        background: #04153E;
        opacity: 1;
      }

      .img-container {
        width: 16px;
        height: 16px;
        margin-right: 12px;
      }
    }
  }
  .arrow-top {
    display: none;
    &.show {
      display: inline;
    }
  }
  .arrow-down {
    display: inline;
    &.show {
      display: none;
    }
  }
  .dropdown-items {
    display: none;

    &.show {
      display: block;
    }
  }
  .dropdown-item {
    padding: 0!important;
    a {
      padding-left: 68px;
    }
  }
}
</style>
