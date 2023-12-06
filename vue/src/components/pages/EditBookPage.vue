<template>
  <PageLayout>
    <section>
      <BookForm />
    </section>
  </PageLayout>
</template>

<script>
import BookForm from "@/components/forms/BookForm.vue";
import PageLayout from "@/components/parts/PageLayout.vue";

export default {
  name: 'EditBookPage',
  components: {
    PageLayout,
    BookForm
  }
}
</script>
