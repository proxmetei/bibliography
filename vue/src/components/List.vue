<template>
    <div>
    <ul v-if="typeOfList=='ul'">
        <li
         v-for="book in books"
         :key="book.id"
        >
        {{book.title}}, {{book.author}}
        </li>
    </ul>
    <ol v-if="typeOfList=='ol'">
        <li
         v-for="book in books"
         :key="book.id"
        >
        {{book.title}}, {{book.author}}
        </li>
    </ol>
    </div>
</template>

<script>

export default {
    name: "ListContainer",
    props: {
        books: {
            type: Array,
            default: () => []
        },
        typeOfList: {
            type: String,
            default: 'ul'
        }
    }
}
</script>
<style>
</style>