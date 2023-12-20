<template>
    <PageLayout>
      <section>
        <div>
          <ElSelect v-model="typeOfList" placeholder="Выберите тип списка">
            <ElOption
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            />
          </ElSelect>
        </div>
        <ListContainerAuthors
          :authors="authors"
          :type-list="typeOfList"
          :is-edit="$route.name===RouteNames.AUTHORS_EDIT"
        />
      </section>
    </PageLayout>
  </template>
  
  <script>
  import {mapGetters} from "vuex";
  import { helpModal } from "@/mixins/modals";
  import ListContainerAuthors from "@/components/parts/biblio/authors/ListAuthors.vue";
  import {RouteNames} from "@/router/routes";
  import PageLayout from "@/components/parts/PageLayout.vue";
  
  export default {
    name: 'AuthorsPage',
    mixins: [helpModal],
    components: {
      PageLayout,
      ListContainerAuthors
    },
    data () {
      return {
        typeOfList: 'ol'
      }
    },
    computed: {
      ...mapGetters('authors', [
        'getAuthors'
      ]),
      RouteNames () {
        return RouteNames
      },
      authors () {
        return this.getAuthors
      },
      options () {
        return [{
          value: "ol",
          label: "Нумерованный список"
        }, {
          value: "ul",
          label: "Простой список"
        }, {
          value: "div",
          label: "Блочный список"
        }]
      }
    }
  }
  </script>
  