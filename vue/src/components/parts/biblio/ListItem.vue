<template>
  <span>
    {{itemString}}
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
    itemString() {
      if (this.book.type == 'book'){
        return `${this.authorBeforeTitle} ${this.title} : `
          + `${this.typeBook} / ${this.authorsAfterTitle} – `
          + `${this.editionNum}${this.city}`
          + `${this.publisher}`
          + `, ${this.year}. – ${this.pagesNum}`
          + ` ${this.isbn}`;
      } else if (this.book.type == 'abstract') {
        return `${this.authorBeforeTitle} ${this.title} : дис. ... `
          + `${this.authorTitle} : ${this.scientificSpecialty} / `
          + `  ${this.authorFullInitials}${this.supervisor}`
          + ` ; ${this.university}. – ${this.city}, ${this.year}`
          + `. – ${this.pagesNum}`
      } else if (this.book.type == 'articleBook') {
        return `${this.authorBeforeTitle} ${this.title}`
          + ` / ${this.authorsAfterTitle} // `
          + `${this.originName}. – ${this.city}, `
          + `${this.year}. – ${this.pages}`
      } else if (this.book.type == 'articleMagazine') {
        return `${this.authorBeforeTitle} ${this.title}`
          + ` / ${this.authorsAfterTitle} // `
          + `${this.originName}. – ${this.year}. – `
          + `${this.magazineNum}. – ${this.pages}`
      } else if (this.book.type == 'web') {
        return `${this.title}. – ${this.url} ${this.viewDate}`;
      } else if(this.book.type == 'articleWeb') {
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