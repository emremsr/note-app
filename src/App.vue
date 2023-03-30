<template>
  <div class="">
    <!-- Modal -->
    <div v-if="showModal" class="fixed z-10 inset-0 overflow-y-auto">
      <div class="flex items-center justify-center min-h-screen px-4">
        <div class="fixed inset-0 transition-opacity" aria-hidden="true">
          <div class="absolute inset-0 bg-gray-500 opacity-75"></div>
        </div>

        <div
          class="bg-white rounded-lg overflow-hidden shadow-xl transform transition-all sm:max-w-lg sm:w-full"
        >
          <div class="bg-gray-100 px-4 py-3">
            <h2 class="text-lg font-semibold text-gray-800">New Note</h2>
          </div>
          <div class="bg-white px-4 pt-5 pb-4 sm:p-6 sm:pb-4">
            <!-- Modal content goes here -->
            <textarea
              v-model="newNotes"
              class="border-2 w-full"
              name="note"
              id="note"
              cols="60"
              rows="10"
            ></textarea>
          </div>
          <div
            class="bg-gray-100 px-4 py-3 sm:px-6 sm:flex sm:flex-row-reverse"
          >
            <button
              :disabled="newNotes.length < 5"
              @click="addNotes"
              class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full sm:ml-3 sm:w-auto w-full sm:text-sm text-base focus:outline-none focus:ring-2 focus:ring-blue-800 mb-2 md:mb-0"
            >
              Save Changes
            </button>
            <button
              @click="showModal = false"
              class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-2 px-4 rounded-full sm:ml-3 sm:w-auto w-full sm:text-sm text-base focus:outline-none focus:ring-2 focus:ring-gray-800"
            >
              Cancel
            </button>
          </div>
        </div>
      </div>
    </div>
    <div class="grid grid-cols-2 place-items-center pt-10">
      <h1 class="text-3xl font-semibold">Notes</h1>

      <button
        @click="showModal = true"
        class="bg-stone-900 hover:bg-stone-700 text-white py-2 px-4 rounded-full"
      >
        +
      </button>
    </div>
    <div
      class="grid grid-cols-1 sm:grid-cols-2 place-items-center md:grid-cols-3 lg:grid-cols-4"
    >
      <div
        v-for="(note, index) in notes"
        :key="index"
        class="flex flex-col justify-between w-64 h-fit border-2 px-5 py-3 md:gap-5 mx-10 my-5 rounded-xl"
        :style="{ backgroundColor: note.backgroudColor }"
      >
        <p>{{ note.text }}</p>
        <p>{{ note.date.toLocaleDateString("tr-TR") }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const showModal = ref(false);

const newNotes = ref("");
const notes = ref([]);

function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}

const addNotes = () => {
  notes.value.push({
    text: newNotes.value,
    date: new Date(),
    backgroudColor: getRandomColor(),
  });
  showModal.value = false;
  newNotes.value = "";
};
</script>

<style scoped></style>
