<template>
  <div>
    <span class="book-form__input__label">Фамимлия автора</span>
    <ElInput
        :value="author.surname"
        placeholder="Укажите фамилию автора"
        class="book-form__input__text"
        @input="(v) => updateSurname(v)"
    />
    <span class="book-form__input__label">Имя автора</span>
    <ElInput
        :value="author.name"
        placeholder="Укажите имя автора"
        class="book-form__input__text"
        @input="(v) => updateName(v)"
    />
    <span class="book-form__input__label">Отчество автора</span>
    <ElInput
        :value="author.patronymic"
        placeholder="Укажите фамимлию автора"
        class="book-form__input__text"
        @input="(v) => updatePatronymic(v)"
    />
  </div>
</template>

<script>
export default {
  name: 'AuthorForm',
  model: {
    prop: 'author',
    event: 'change'
  },
  props: {
    author: {
      type: Object,
      required: true,
      default: () => {
        return {
          surname: "",
          name: "",
          patronymic: ""
        }
      }
    }
  },
  methods: {
    updateSurname (v) {
      this.$emit('change', {
        ...this.author,
        surname: v
      })
    },
    updateName (v) {
      this.$emit('change', {
        ...this.author,
        name: v
      })
    },
    updatePatronymic (v) {
      this.$emit('change', {
        ...this.author,
        patronymic: v
      })
    }
  }
}
</script>
