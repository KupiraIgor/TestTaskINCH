<script setup>
import { ref } from 'vue'
import { useVuelidate } from '@vuelidate/core'
import { required, helpers } from '@vuelidate/validators'

import Input from '@/components/Base/Input.vue'
import InputRadio from '@/components/Base/InputRadio.vue'

const radioButtons = [
  { id: 1, name: 'СПОЖИВАЧ' },
  { id: 2, name: 'МЕДИЧНИЙ ПРАЦІВНИК' },
  { id: 3, name: 'ЖурналІст' }
]
const formData = ref({
  lastName: '',
  firstName: '',
  organization: '',
  position: 1,
  themeMessage: '',
  message: '',
  email: '',
  country: '',
  city: '',
  index: '',
  address: '',
  phone: ''
})

const onlyCyrillicRegex = /^[А-Яа-яЁёІіЇїЄєҐґ]+$/
const onlyNumbersRegex = /^\d+$/
const cyrillicNumbersSymbolsRegex = /^[А-Яа-яЁёІіЇїЄєҐґ\d\/,-]+$/
const cyrillicNumbersRegex = /^[А-Яа-яЁёІіЇїЄєҐґ\d]+$/

const rulesValidate = {
  lastName: {
    required,
    cyrillicRegex: helpers.regex(onlyCyrillicRegex)
  },
  firstName: { required, cyrillicRegex: helpers.regex(onlyCyrillicRegex) },
  organization: {
    cyrillicRegex: helpers.regex(onlyCyrillicRegex)
  },
  position: {},
  themeMessage: {
    cyrillicRegex: helpers.regex(onlyCyrillicRegex)
  },
  message: { required, cyrillicAndNumbersRegex: helpers.regex(cyrillicNumbersRegex) },
  email: { required, cyrillicAndNumbersRegex: helpers.regex(cyrillicNumbersRegex) },
  country: {
    cyrillicRegex: helpers.regex(onlyCyrillicRegex)
  },
  city: {
    cyrillicRegex: helpers.regex(onlyCyrillicRegex)
  },
  index: { numbersRegex: helpers.regex(onlyNumbersRegex) },
  address: { cyrillicNumbersAndSymbolsRegex: helpers.regex(cyrillicNumbersSymbolsRegex) },
  phone: { required }
}

const v$ = useVuelidate(rulesValidate, formData)

const onSubmit = async () => {
  formData.value.phone = formData.value.phone.replace(/\D/g, '')
  const result = await v$.value.$validate()

  if (result) {
    alert('Відправлено')
  }
}
</script>

<template>
  <div class="form">
    <div class="container">
      <form class="form__body" @submit.prevent="onSubmit">
        <div class="form__col">
          <h2 class="form__title">ПРЕДСТАВТЕСЯ, БУДЬ ЛАСКА</h2>
          <Input
            v-model="formData.lastName"
            placeholder="Прізвище"
            required
            :error="v$.lastName.$errors.length"
          />
          <Input
            v-model="formData.firstName"
            placeholder="ІМ’Я"
            required
            :error="v$.firstName.$errors.length"
          />
          <Input
            v-model="formData.organization"
            placeholder="ОрганІзацІя ТА ПОСАДА"
            :error="v$.organization.$errors.length"
          />
          <div class="form__radios">
            <InputRadio v-model="formData.position" v-for="item of radioButtons" :data="item" />
          </div>
          <h2 class="form__title">ПОВІДОМЛЕННЯ</h2>
          <Input
            v-model="formData.themeMessage"
            placeholder="Тема ПОВІДОМЛЕННЯ"
            :error="v$.themeMessage.$errors.length"
          />
          <Input
            v-model="formData.message"
            placeholder="ПОВІДОМЛЕННЯ"
            required
            textarea
            :error="v$.message.$errors.length"
          />
        </div>
        <div class="form__col">
          <h2 class="form__title">Контактна Інформація</h2>
          <Input
            v-model="formData.email"
            placeholder="Email"
            required
            :error="v$.email.$errors.length"
          />
          <Input
            v-model="formData.country"
            placeholder="КРАЇНА"
            :error="v$.country.$errors.length"
          />
          <Input v-model="formData.city" placeholder="МІСТО" :error="v$.city.$errors.length" />
          <Input v-model="formData.index" placeholder="ІНДЕКС" :error="v$.index.$errors.length" />
          <Input
            v-model="formData.address"
            placeholder="АдресА"
            :error="v$.address.$errors.length"
          />
          <Input
            v-model="formData.phone"
            placeholder="Телефон"
            :error="v$.phone.$errors.length"
            required
            phone
          />
          <button class="form__button" type="submit">відправити</button>
        </div>
      </form>
    </div>
  </div>
</template>

<style scoped lang="scss">
.form {
  &__body {
    display: flex;
    justify-content: center;
    gap: 20rem;
  }

  &__col {
    max-width: 25rem;
    width: 100%;
    flex-shrink: 0;
    display: flex;
    flex-direction: column;
    gap: 1rem;
    justify-content: space-between;
  }

  &__title {
    font-size: 1.8rem;
    font-weight: 400;
    text-transform: uppercase;
    white-space: nowrap;

    &:first-child {
      margin-bottom: 3rem;
    }
  }

  &__radios {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
  }

  &__button {
    font-size: 2.2rem;
    min-height: 3rem;
    width: 100%;
    text-align: center;
    color: var(--color-white);
    background: #444;
  }

  @media (max-width: 1000px) {
    &__body {
      gap: 5rem;
    }

    &__title {
      &:first-child {
        margin-bottom: 0;
      }
    }
  }

  @media (max-width: 768px) {
    &__body {
      flex-direction: column;
      gap: 1rem;
    }
  }
}
</style>
