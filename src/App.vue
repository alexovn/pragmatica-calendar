<template>
  <div class="wrapper">
    <main class="main">
      <div class="page-calendar">
        <div class="breadcrumbs">
          <div class="container">
            <ul class="breadcrumbs__list">
              <li class="breadcrumbs__item">Главная</li>
              <li class="breadcrumbs__item">Сервисы</li>
              <li class="breadcrumbs__item active">Планирование</li>
            </ul>
          </div>
        </div>
        <div class="page__title title">
          <div class="container">
            <h1>
              Планирование
            </h1>
          </div>
        </div>
        <div class="calendar-block">
          <div class="container">
            <div class="calendar-block__content">
              <calendar></calendar>
              <div class="employees-info">
                <div class="employees-info-item">
                  <div class="employee-select">
                    <div class="employee-select__title">
                      Сотрудник
                    </div>
                    <employee-select :users="users"></employee-select>
                  </div>
                </div>
                <div class="employees-info-item">
                  <employee-events></employee-events>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import calendar from './components/calendar.vue'
import employeeSelect from './components/employee-select.vue'
import employeeEvents from './components/employee-events.vue'

export default {
  name: 'App',
  components: {
    calendar: calendar,
    'employee-select': employeeSelect,
    'employee-events': employeeEvents
  },
  data () {
    return {
      users: [
        {
          img: require('@/assets/img/user-pics/image-1.jpg'),
          name: 'Алексей Лечащий',
          eventList: [
            {
              city: 'Екатеринбург',
              cityColor: '#0071B2',
              dates: ['2021-06-01', '2021-06-02']
            },
            {
              city: 'Москва',
              cityColor: '#59A646',
              dates: ['2021-06-04', '2021-06-07']
            },
            {
              city: 'Санкт-Петербург',
              cityColor: '#AF032C',
              dates: ['2021-06-04', '2021-06-07']
            },
            {
              city: 'Сочи',
              cityColor: '#DE911D',
              dates: ['2021-06-28', '2021-06-29', '2021-06-30']
            }
          ]
        },
        {
          img: require('@/assets/img/user-pics/image-1.jpg'),
          name: 'Дима Муха'
        },
        {
          img: require('@/assets/img/user-pics/image-1.jpg'),
          name: 'Саша Кощей'
        },
        {
          img: require('@/assets/img/user-pics/image-1.jpg'),
          name: 'Петя Стреляный'
        },
        {
          img: require('@/assets/img/user-pics/image-1.jpg'),
          name: 'Маша Лишняя'
        }
      ]
    }
  }
}
</script>

<style lang="scss">
@import "./assets/styles/index.scss";

:root {
  --day-border: 1px solid #e9e9e9;
}

.title {
  font-weight: 700;
  color: #002033;
}

.page {
  &__title {
    margin: 0 0 2.32rem;
    @include text72;
  }
}

.page-calendar {
  padding-bottom: 18.13rem;
}

.breadcrumbs {
  padding: 2.44rem 0 0.94rem;
  &__list {
    display: flex;
    align-items: center;
    @include text18;
    color: rgba(0, 32, 51, 0.6);
  }

  &__item {
    padding-right: 1.33rem;
    margin-right: 1.22rem;
    position: relative;

    &:not(:last-child) {
      &::after {
        content: "";
        position: absolute;
        top: 50%;
        right: 0;
        transform: translate(0, -50%);
        width: 7px;
        height: 11px;
        background: url("./assets/img/icons/icon-arrow.svg") 0 / contain
          no-repeat;
      }
    }

    &.active {
      color: #000;
    }
  }
}

.calendar-block {
  &__content {
    display: grid;
    grid-template-columns: 2.1fr 1fr;
    gap: 1.875rem;
  }
}

.employees-info {
  &-item {
    &:not(:last-child) {
      margin-bottom: 0.625rem;
    }
    border-radius: 0.44rem;
    background: #fff;
  }
}

.employee-select {
  padding: 1.625rem 2rem;
  &__title {
    margin-bottom: 1.31rem;
    font-size: 1.375rem;
    font-weight: bold;
  }
}
</style>
