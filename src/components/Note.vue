<template>
  <article
    :class="item['color']"
    v-for="(item, index) in notes"
    :key="index"
    class="shadow-xl max-w-sm p-6 transform duration-500 hover:-translate-y-2 rounded-md"

  >
    <p class="text-md  cursor-pointer font-semibold leading-relaxed  pb-6 text-black"     @click="$emit('updateNote',item['id'])">
      {{item['note']}}
    </p>
    <div class="mt-5 flex justify-between items-center">
      <a class="cursor-pointer" @click="$emit('deleteNote',item['id'])">
        <svg
          xmlns="http://www.w3.org/2000/svg "
          class="h-6 w-6 text-gray-400"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"
          /></svg
      ></a>

      <p class="text-right text-sm text-gray-400 font-bold">
        {{item['createdDate']}}
      </p>
    </div>
  </article>
</template>

<script>
export default {
    props:['notes'],

}
</script>

<style></style>
