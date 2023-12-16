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
      default: () => ({})
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
    strBook() {
      return `${this.authorBeforeTitle} ${this.title} : `
        + `${this.typeBook} / ${this.authorsAfterTitle} – `
        + `${this.editionNum}${this.city}`
        + `${this.publisher}`
        + `, ${this.year}. – ${this.pagesNum}`
        + ` ${this.isbn}`;
    },
    strAbstract() {
      return `${this.authorBeforeTitle} ${this.title} : дис. ... `
        + `${this.authorTitle} : ${this.scientificSpecialty} / `
        + `  ${this.authorFullInitials}${this.supervisor}`
        + ` ; ${this.university}. – ${this.city}, ${this.year}`
        + `. – ${this.pagesNum}`
    },
    strArticleBook() {
      return `${this.authorBeforeTitle} ${this.title}`
        + ` / ${this.authorsAfterTitle} // `
        + `${this.originName}. – ${this.city}, `
        + `${this.year}. – ${this.pages}`
    },
    strArticleMagazine() {
      return `${this.authorBeforeTitle} ${this.title}`
        + ` / ${this.authorsAfterTitle} // `
        + `${this.originName}. – ${this.year}. – `
        + `${this.magazineNum}. – ${this.pages}`
    },
    strWeb() {
      return `${this.title}. – ${this.url} ${this.viewDate}`
    },
    strArticleWeb() {
      return `${this.authorBeforeTitle} ${this.title}`
        + `${this.authorsAfterTitle} // ${this.originName}. – ${this.year}`
        + `. – ${this.url} ${this.viewDate}`
    },
    itemString() {
      if (this.isBook){
        return this.strBook
      } else if (this.isAbstract) {
        return this.strAbstract
      } else if (this.isArticleBook) {
        return this.strArticleBook
      } else if (this.isArticleMagazine) {
        return this.strArticleMagazine
      } else if (this.isWeb) {
        return this.strWeb
      } else if(this.isArticleWeb) {
        return this.strArticleWeb
      } else {
        return ``;
      }
    }
  }
}
</script>

<style></style>