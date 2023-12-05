<template>
  <div>
    <component :is="typeList">
      <li
        v-for="book in books" 
        :key="book.id" 
        :style="cssProps"
      >
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
        <el-button
            v-if="isEdit"
            type="danger"
            icon="el-icon-delete"
            circle
            @click="() => deleteBook(book)"
        />
      </li>
    </component>
  </div>
</template>

<script>
import {mapActions} from "vuex";

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
