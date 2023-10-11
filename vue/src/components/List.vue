<template>
    <div>
        <component :is="typeList">
            <li
                v-for="book in books"
                :key="book.id"
            >
                {{ book.title }}, {{ book.author }}
            </li>
        </component>
    </div>
</template>

<script>

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
        }
    }
}
</script>
<style></style>