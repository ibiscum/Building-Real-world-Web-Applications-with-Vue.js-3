<template>
    <div>  
      <LoadingIndicator v-if="isSearching" :text="'Searching by \'' + searchQuery + '\'...'" />
      <div v-if="data && data.length > 0 && !isSearching && query">
        <div
          class="grid grid-flow-row grid-cols-1 gap-4 sm:grid-cols-2 lg:grid-cols-4"
        >
          <CharacterCard
            :character="character"
            :key="character.id"
            v-for="character in data"
          ></CharacterCard>
        </div>
        <Pagination
          :total-pages="totalPages"
          :path="'/search/' + searchQuery + '/'"
          :current-page="currentPage"
        ></Pagination>
      </div>
      <div
        v-if="data && data.length === 0 && query"
        class="flex flex-col items-center justify-center p-4 pt-16 min-h-min min-w-screen"
      >
        <div class="mb-4">
          <p>
            🦹 Nothing found for "<em class="font-bold">{{ searchQuery }}</em
            >". Please try again! 🦸‍♂️
          </p>
        </div>
      </div>
    </div>
    </template>
  
  <script>
  export default {
    data() {
      return {
        isSearching: false,
        // Add other properties like searchQuery, data, query, totalPages, currentPage as needed
        searchQuery: '',
        data: [],
        query: '',
        totalPages: 1,
        currentPage: 1
      };
    },
    // Add methods, computed, and lifecycle hooks as needed
  };
  </script>