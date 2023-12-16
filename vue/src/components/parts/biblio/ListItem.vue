<template>
  <span>
    {{ itemString }}
  </span>
</template>
<script>

export default {
  name: "ListItem",
  props: {
    book: {
      type: Object,
      default: null
    }
  },
  computed: {
    pagesNum() {
      return `${this.book.pagesNum} с.`
    },
    pages() {
      return `С. ${this.book.pages}`
    },
    editionNum() {
      return `${this.book.editionNum ? `${this.book.editionNum} -е изд. – ` : ``}`
    },
    supervisor() {
      return `${this.book.supervisor ? ` ; науч. рук. ${this.book.supervisor}` : ``}`
    },
    magazineNum() {
      return `№${this.book.magazineNum}`
    },
    viewDate() {
      return `(дата обращения: ${this.book.viewDate})`
    },
    publisher() {
      return `${this.book.publisher ? ` : ${this.book.publisher}` : ``}`
    },
    url() {
      return `URL: ${this.book.url}`
    },
    authorBeforeTitle() {
      return `${this.book.authors[0].name} ${this.book.authors[0].initials}`
    },
    authorsAfterTitle() {
      return `${this.book.authors.reduce((acc, curr, index) => {
        return acc + `${curr.initials} ${curr.name}${index == this.book.authors.length - 1 ? '.' : ', '}`;
      }, '')}`
    },
    authorFullInitials() {
      return `${this.book.authors[0].name} ${this.book.fullInitials}`
    },
    isbn() {
      return `${this.book.isbn ? ` – ISBN ${this.book.isbn}` : ``}`
    },
    year() {
      return `${this.book.year}`
    },
    city() {
      return `${this.book.city}`
    },
    title() {
      return `${this.book.title}`
    },
    originName() {
      return `${this.book.originName}`
    },
    typeBook() {
      return `${this.book.typeBook}`
    },
    authorTitle() {
      return `${this.book.authorTitle}`
    },
    scientificSpecialty() {
      return `${this.book.scientificSpecialty}`
    },
    university() {
      return `${this.book.university}`
    },
    type() {
      return this.book.type
    },
    isBook() {
      return this.type == 'book'
    },
    isAbstract() {
      return this.type == 'abstract'
    },
    isArticleBook() {
      return this.type == 'articleBook'
    },
    isArticleMagazine() {
      return this.type == 'articleMagazine'
    },
    isWeb() {
      return this.type == 'web'
    },
    isArticleWeb() {
      return this.type == 'articleWeb'
    },
    itemString() {
      if (this.isBook){
        return `${this.authorBeforeTitle} ${this.title} : `
          + `${this.typeBook} / ${this.authorsAfterTitle} – `
          + `${this.editionNum}${this.city}`
          + `${this.publisher}`
          + `, ${this.year}. – ${this.pagesNum}`
          + ` ${this.isbn}`;
      } else if (this.isAbstract) {
        return `${this.authorBeforeTitle} ${this.title} : дис. ... `
          + `${this.authorTitle} : ${this.scientificSpecialty} / `
          + `  ${this.authorFullInitials}${this.supervisor}`
          + ` ; ${this.university}. – ${this.city}, ${this.year}`
          + `. – ${this.pagesNum}`
      } else if (this.isArticleBook) {
        return `${this.authorBeforeTitle} ${this.title}`
          + ` / ${this.authorsAfterTitle} // `
          + `${this.originName}. – ${this.city}, `
          + `${this.year}. – ${this.pages}`
      } else if (this.isArticleMagazine) {
        return `${this.authorBeforeTitle} ${this.title}`
          + ` / ${this.authorsAfterTitle} // `
          + `${this.originName}. – ${this.year}. – `
          + `${this.magazineNum}. – ${this.pages}`
      } else if (this.isWeb) {
        return `${this.title}. – ${this.url} ${this.viewDate}`;
      } else if(this.isArticleWeb) {
        return `${this.authorBeforeTitle} ${this.title}`
          + `${this.authorsAfterTitle} // ${this.originName}. – ${this.year}`
          + `. – ${this.url} ${this.viewDate}`
      } else {
        return ``;
      }
    }
  }
}
</script>

<style></style>