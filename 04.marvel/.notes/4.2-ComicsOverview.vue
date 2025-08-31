<script lang="ts" setup>
import { ref, onMounted } from "vue";
import type { Ref } from "vue";
import { useRoute } from "vue-router";

import { useComics } from "../src/composables/marvelApi";
import type { Comic } from "../src/types/marvel";

import LoadingIndicator from "../src/components/LoadingIndicator.vue";
import ComicCard from "../src/components/ComicCard.vue";

const route = useRoute();

const isLoading: Ref<boolean> = ref(false);
const data: Ref<Comic[] | undefined> = ref();
const currentPage: Ref<number | string> = ref(0);
const totalPages: Ref<number> = ref(0);

if (route.params.page) {
  currentPage.value = +route.params.page;
}

const getComics = async () => {
  isLoading.value = true;
  const comics = await useComics();

  currentPage.value = comics?.offset / comics?.limit || 0;
  totalPages.value = Math.ceil(comics.total / comics.limit);

  data.value = comics.results;
  isLoading.value = false;
};

onMounted(async () => {
  await getComics();
});
</script>
