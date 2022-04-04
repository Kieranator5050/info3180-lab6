<script>

import NewsList from '@/components/NewsList.vue'

export default {
    data() {
        return {};
    },
    components: { NewsList }
};
</script>

<template>
    <div class="news container">
      <div class="text-center">
        <h2>News</h2>
        <NewsList />
      </div>
    </div>
</template>

<style>
</style>