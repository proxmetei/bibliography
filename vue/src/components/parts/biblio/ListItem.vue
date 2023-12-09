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
    itemString() {
      if (this.book.type == 'book'){
        return `${this.book.authors[0].name} ${this.book.authors[0].initials} ${this.book.title} : `
          + `${this.book.typeBook} / ${this.book.authors[0].initials} ${this.book.authors[0].name}. – `
          + `${this.book.editionNum ? `${this.book.editionNum} -е изд. – ` : ``}${this.book.city}`
          + `${this.book.publisher ? ` : ${this.book.publisher}` : ``}`
          + `, ${this.book.year}. – ${this.book.pagesNum}`
          + ` с.${this.book.isbn ? ` – ISBN ${this.book.isbn}` : ``}`;
      } else if (this.book.type == 'abstract') {
        return `${this.book.authors[0].name} ${this.book.authors[0].initials} ${this.book.title} : дис. ... `
          + `${this.book.authorTitle} : ${this.book.scientificSpecialty} / ${this.book.authors[0].name}`
          + `  ${this.book.fullInitials}${this.book.supervisor ? ` ; науч. рук. ${this.book.supervisor}` : ``}`
          + ` ; ${this.book.university}. – ${this.book.city}, ${this.book.year}`
          + `. – ${this.book.pagesNum} с.`
      } else if (this.book.type == 'articleBook') {
        return `${this.book.authors[0].name} ${this.book.authors[0].initials} ${this.book.title}`
          + ` / ${this.book.authors[0].initials} ${this.book.authors[0].name} // `
          + `${this.book.originName}. – ${this.book.city}, `
          + `${this.book.year}. – С. ${this.book.pages}`
      } else if (this.book.type == 'articleMagazine') {
        return `${this.book.authors[0].name} ${this.book.authors[0].initials} ${this.book.title}`
          + ` / ${this.book.authors[0].initials} ${this.book.authors[0].name} // `
          + `${this.book.originName}. – ${this.book.year}. – №`
          + `${this.book.magazineNum}. – С. ${this.book.pages}`
      } else if (this.book.type == 'web') {
        return `${this.book.title}. – URL: ${this.book.url} (дата обращения: ${this.book.viewDate})`;
      } else if(this.book.type == 'articleWeb') {
        return `${this.book.authors[0].name} ${this.book.authors[0].initials} ${this.book.title}`
          + `${this.book.authors[0].initials}${this.book.authors[0].name} // ${this.book.originName}. – ${this.book.year}`
          + `. – URL: ${this.book.url} (дата обращения: ${this.book.viewDate})`
      } else {
        return ``;
      }
    }
  }
}
</script>
<style></style>