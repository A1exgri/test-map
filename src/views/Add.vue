<template>
  <div class="add-page">
    <div class="row">
      <div class="col-6">
        <div class="breadcrumb">
          <router-link to="/">
            <img class="arrow-back" src="/img/project-icons/arrow-back.svg"/>Назад
          </router-link>
        </div>
      </div>
      <div class="col-6">
        <div class="manager">
          <img class="manager__img" src="/img/manager.png"/>
          <div>
            <div class="manager__name">Александра</div>
            <div class="manager__position">Должность</div>
          </div>
        </div>
      </div>
    </div>
    <h2 class="main-title">Добавление организации</h2>
    <p class="middle-text">Поставщик</p>
    <div class="row">
      <div class="col-md-6">
        <input
            class="input"
            :class="v$.organization.name.$error ? 'invalid' : ''"
            v-model.trim="organization.name"
            placeholder="Наименование организации"
            type="text"
        >
        <div v-if="v$.organization.name.$error" class="alert alert-danger" role="alert">
          Заполните "Наименование организации", оно должно иметь не менее 3 символов
        </div>
        <input
            class="input"
            :class="v$.organization.email.$error ? 'invalid' : ''"
            v-model.trim="organization.email"
            placeholder="Имейл"
            type="email"
        >
        <div v-if="v$.organization.email.$error" class="alert alert-danger" role="alert">
          Заполните поле "Email" корректно
        </div>
        <select
            class="select"
            v-model="organization.statusChecked"
            :class="v$.organization.statusChecked.$error ? 'invalid' : ''"
        >
          <option disabled value="">Статус</option>
          <option
              v-for="(status, index) in organization.status"
              :key="index"
              :value="status.value"
          >
            {{ status.label }}
          </option>
        </select>
        <div v-if="v$.organization.statusChecked.$error" class="alert alert-danger" role="alert">
          Поле "Статус" обязательно для заполнения
        </div>
      </div>
      <div class="col-md-6">
        <div class="map">
          <img src="/img/map.jpg" alt="map">
        </div>
      </div>
      <div class="col-12">
        <button class="btn btn-submit" type="submit" @click="submit">Сохранить</button>
      </div>
    </div>

  </div>
</template>

<script>
import { useVuelidate } from '@vuelidate/core'
import { required, email, minLength } from '@vuelidate/validators'

export default {
  name: "Add",
  data() {
    return {
      organization: {
        name: '',
        email: '',
        status: [
          { label: 'Статус 1', value: 'status1'},
          { label: 'Статус 2', value: 'status2'},
          { label: 'Статус 3', value: 'status3'},
        ],
        statusChecked: ''
      },
    }
  },
  setup: () => ({ v$: useVuelidate() }),
  validations: {
      organization: {
        name: { required,  minLength: minLength(3)},
        email: { required, email },
        statusChecked: { required }
    }
  },
    methods: {
      submit() {
        this.v$.organization.$touch()
        if(!this.v$.organization.$error) {
          console.log('Данные орагнизации: ', this.organization)
        }
      }
    }
  }
</script>
<style lang="scss">
  .add-page {
    max-width: 1074px;
    .main-title {
      font-weight: 800;
      font-size: 28px;
      line-height: 32px;
      color: #04153E;
      margin: 0px 4px 8px;
    }
    .middle-text {
      font-size: 16px;
      line-height: 20px;
      color: rgba(4, 21, 62, .48)
    }
    .breadcrumb {
      a {
        display: flex;
        align-items: center;
        font-weight: 500;
        font-size: 16px;
        line-height: 20px;
        color: #3D75E4;
        text-decoration: none;

        img {
          margin-right: 9px;
        }
      }
    }
    .manager {
      display: flex;
      align-items: center;

      &__img {
        height: 40px;
        width: 40px;
        margin-right: 8px;
      }
      &__name {
        font-weight: 800;
        font-size: 13px;
        line-height: 16px;
        color: #04153E;
      }
      &__position {
        font-weight: normal;
        font-size: 10px;
        line-height: 12px;
        color: #04153E;
        opacity: 0.72;
      }
    }
    .input {
      width: 100%;
      background: rgba(61, 117, 228, .08);
      border:0;
      border-radius: 8px;
      padding: 10px 16px;
      font-size: 16px;
      line-height: 20px;
      color: rgba(4, 12, 62, .48);
      margin-top: 12px;
      margin-bottom: 12px;
      &.invalid {
        border: 2px solid #842029;
      }
    }
    .select {
      display: block;
      font-size: 16px;
      color: rgba(4, 12, 62, 0.48);
      line-height: 20px;
      border-radius: 8px;
      padding: 10px 16px;
      width: 100%;
      max-width: 100%;
      box-sizing: border-box;
      margin-top: 12px;
      margin-bottom: 12px;
      border: 0;
      -moz-appearance: none;
      -webkit-appearance: none;
      appearance: none;
      background-color: rgba(61, 117, 228, 0.08);
      background-image: url('/img/project-icons/arrow-bottom.svg');
      background-repeat: no-repeat, repeat;
      background-position: right .7em top 50%, 0 0;
      background-size: 20px auto, 100%;
    }
    .select::-ms-expand { display: none; }
    .select:hover { border-color: #888; }
    .selects:focus { border-color: #aaa;
      color: #222;
      outline: none;
    }
    .select option {
      font-weight:normal;
    }

    .alert {
      padding: 5px 16px;
      font-size: 12px
    }
    .btn-submit {
      padding: 10px 16px;
      width: 100%;
      background: rgba(61, 117, 228, 0.48);
      color: #fff;
      border-radius: 8px;
      &:hover {
        background: #3D75E4;
      }
    }
    .map {
      text-align: right;
      margin-top: 12px;
      margin-bottom: 32px;

      img {
        object-fit: cover;
        width: 100%;
        height: 480px;
      }
    }
  }
</style>
