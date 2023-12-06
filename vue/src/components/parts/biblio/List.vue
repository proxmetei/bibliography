<template>
  <div class="list-container__wrapper">
    <Component :is="typeList" class="list-container">
      <li
        v-for="book in books"
        :key="book.id"
        :style="cssProps"
      >
        <div v-if="isEdit" class="list-container__item">
          <template v-if="book.type == 'book'">
            <span>
              {{ 
                `${book.author} ${book.initials} ${book.title} : `
                + `${book.typeBook} / ${book.initials} ${book.author}. – `
                + `${book.editionNum ? `${book.editionNum} -е изд. – ` : ``}${book.city}`
                + `${book.publisher ? ` : ${book.publisher}` : ``}`
                + `, ${book.year}. – ${book.pagesNum}`
                + ` с.${book.isbn ? ` – ISBN ${book.isbn}` : ``}`
              }}
            </span>
          </template>
          <template v-else-if="book.type == 'abstract'">
            <span>
              {{ 
                `${book.author} ${book.initials} ${book.title} : дис. ... `
                + `${book.authorTitle} : ${book.scientificSpecialty} / ${book.author}`
                + `  ${book.fullInitials}${book.supervisor ? ` ; науч. рук. ${book.supervisor}` : ``}`
                + ` ; ${book.university}. – ${book.city}, ${book.year}`
                + `. – ${book.pagesNum} с.`
              }}
            </span>
          </template>
          <template v-else-if="book.type == 'articleBook'">
            <span>
              {{ 
                `${book.author} ${book.initials} ${book.title}`
                + ` / ${book.initials} ${book.author} // `
                + `${book.originName}. – ${book.city}, `
                + `${book.year}. – С. ${book.pages}`
              }}
            </span>
          </template>
          <template v-else-if="book.type == 'articleMagazine'">
            <span>
              {{ 
                `${book.author} ${book.initials} ${book.title}`
                + ` / ${book.initials} ${book.author} // `
                + `${book.originName}. – ${book.year}. – №`
                + `${book.magazineNum}. – С. ${book.pages}`
              }}
            </span>
          </template>
          <template v-else-if="book.type == 'web'">
            <span>
              {{ 
                `${book.title}. – URL: ${book.url} (дата обращения: ${book.viewDate})`
              }}
            </span>
          </template>
          <template v-else-if="book.type == 'articleWeb'">
            <span>
              {{  
                `${book.author} ${book.initials} ${book.title}`
                + `${book.initials}${book.author} // ${book.originName}. – ${book.year}`
                + `. – URL: ${book.url} (дата обращения: ${book.viewDate})`
              }}
            </span>
          </template>
          <div class="list-container__item__actions">
            <RouterLink :to="{ name: RouteNames.BOOK_EDIT, params: { id: book.id } } ">
              <div class="list-container__item__actions__button">
                <ElButton
                  type="primary"
                  icon="el-icon-edit"
                  size="mini"
                  circle
                />
              </div>
            </RouterLink>
            <ElButton
              type="danger"
              icon="el-icon-delete"
              size="mini"
              circle
              class="list-container__item__actions__button"
              @click="() => deleteBook(book)"
            />
          </div>
        </div>
        <template v-else>
          <template v-if="book.type == 'book'">
            <span>
              {{ 
                `${book.author} ${book.initials} ${book.title} : `
                + `${book.typeBook} / ${book.initials} ${book.author}. – `
                + `${book.editionNum ? `${book.editionNum} -е изд. – ` : ``}${book.city}`
                + `${book.publisher ? ` : ${book.publisher}` : ``}`
                + `, ${book.year}. – ${book.pagesNum}`
                + ` с.${book.isbn ? ` – ISBN ${book.isbn}` : ``}`
              }}
            </span>
          </template>
          <template v-else-if="book.type == 'abstract'">
            <span>
              {{ 
                `${book.author} ${book.initials} ${book.title} : дис. ... `
                + `${book.authorTitle} : ${book.scientificSpecialty} / ${book.author}`
                + `  ${book.fullInitials}${book.supervisor ? ` ; науч. рук. ${book.supervisor}` : ``}`
                + ` ; ${book.university}. – ${book.city}, ${book.year}`
                + `. – ${book.pagesNum} с.`
              }}
            </span>
          </template>
          <template v-else-if="book.type == 'articleBook'">
            <span>
              {{ 
                `${book.author} ${book.initials} ${book.title}`
                + ` / ${book.initials} ${book.author} // `
                + `${book.originName}. – ${book.city}, `
                + `${book.year}. – С. ${book.pages}`
              }}
            </span>
          </template>
          <template v-else-if="book.type == 'articleMagazine'">
            <span>
              {{ 
                `${book.author} ${book.initials} ${book.title}`
                + ` / ${book.initials} ${book.author} // `
                + `${book.originName}. – ${book.year}. – №`
                + `${book.magazineNum}. – С. ${book.pages}`
              }}
            </span>
          </template>
          <template v-else-if="book.type == 'web'">
            <span>
              {{ 
                `${book.title}. – URL: ${book.url} (дата обращения: ${book.viewDate})`
              }}
            </span>
          </template>
          <template v-else-if="book.type == 'articleWeb'">
            <span>
              {{  
                `${book.author} ${book.initials} ${book.title}`
                + `${book.initials}${book.author} // ${book.originName}. – ${book.year}`
                + `. – URL: ${book.url} (дата обращения: ${book.viewDate})`
              }}
            </span>
          </template>
        </template>
      </li>
    </component>
  </div>
</template>

<script>
import {mapActions} from "vuex";
import {RouteNames} from "@/router/routes";

export default {
  name: "ListContainer",
  props: {
    books: {
      type: Array,
      default: () => ([])
    },
    typeList: {
      type: String,
      default: 'ul'
    },
    isEdit: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    RouteNames () {
      return RouteNames
    },
    cssProps () {
      return this.typeList == "div" ? {
        'display': 'block'
      } : {}
    }
  },
  methods: {
    ...mapActions('books', [
      'removeBook'
    ]),
    deleteBook (book) {
      this.removeBook(book.id)
    }
  },
}
</script>

<style scoped lang="less">
.list-container {
  &__wrapper {
    padding: 10px;
  }

  &__item {
    display: flex;

    &__text {
      flex: 1;
    }

    &__actions {
      display: flex;

      &__button {
        margin: 2px;
      }
    }
  }
}
</style>
