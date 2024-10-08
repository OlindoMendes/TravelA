<template>
  <div class="bg-gray-100">
    <section class="bg-white py-16">
      <div class="container mx-auto px-4 text-center">
        <h1 class="text-4xl font-bold text-gray-800">
          Find Your Perfect Hotel
        </h1>
        <p class="text-gray-600 mt-4">
          Book hotels at the best prices with ease.
        </p>

        <form class="mt-8 max-w-full mx-auto">
          <div
            class="flex flex-col sm:flex-row items-center space-y-2 sm:space-y-0 sm:space-x-4"
          >
            <input
              type="text"
              placeholder="Where are you going ? Search here..."
              v-model="destination"
              class="w-full h-12 p-3 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-300"
            />
            <input
              type="date"
              placeholder="check in"
              v-model="checkInDate"
              class="w-full h-12 p-3 border border-gray-300 rounded-md focus:outline-none focus:ring-1 focus:ring-blue-300"
            />
            <input
              type="date"
              placeholder="check out"
              v-model="checkOutDate"
              class="w-full h-12 p-3 border border-gray-300 rounded-md focus:outline-none focus:ring-1 focus:ring-blue-300"
            />
            <div class="relative inline-block text-left w-full">
              <button
                @click="toggleDropdown"
                class="inline-flex justify-between items-center w-full h-12 rounded-md border border-gray-300 shadow-sm p-3 bg-white text-sm font-medium text-gray-700 hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-2 focus:ring-blue-300"
              >
                Select Guests and Rooms
                <svg
                  class="-mr-1 ml-2 h-5 w-5"
                  xmlns="http://www.w3.org/2000/svg"
                  viewBox="0 0 20 20"
                  fill="currentColor"
                >
                  <path
                    fill-rule="evenodd"
                    d="M10 12a1 1 0 01-.7-.29l-5-5a1 1 0 111.4-1.42L10 9.58l4.3-4.29a1 1 0 111.4 1.42l-5 5A1 1 0 0110 12z"
                    clip-rule="evenodd"
                  />
                </svg>
              </button>

              <div
                v-if="isOpen"
                class="origin-top-right absolute right-0 mt-2 w-56 rounded-md shadow-lg bg-white ring-1 ring-black ring-opacity-5 focus:outline-none z-10"
              >
                <div class="py-1 px-4">
                  <!-- Adults -->
                  <div class="flex items-center justify-between py-2">
                    <label
                      for="adults"
                      class="block text-sm font-medium text-gray-700"
                      >Adults</label
                    >
                    <input
                      v-model.number="adults"
                      type="number"
                      min="1"
                      id="adults"
                      class="w-16 p-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 text-center"
                    />
                  </div>

                  <!-- Children -->
                  <div class="flex items-center justify-between py-2">
                    <label
                      for="children"
                      class="block text-sm font-medium text-gray-700"
                      >Children</label
                    >
                    <input
                      v-model.number="children"
                      type="number"
                      min="0"
                      id="children"
                      class="w-16 p-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 text-center"
                    />
                  </div>

                  <!-- Rooms -->
                  <div class="flex items-center justify-between py-2">
                    <label
                      for="rooms"
                      class="block text-sm font-medium text-gray-700"
                      >Rooms</label
                    >
                    <input
                      v-model.number="rooms"
                      type="number"
                      min="1"
                      id="rooms"
                      class="w-16 p-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 text-center"
                    />
                  </div>

                  <!-- Save Button -->
                  <div class="flex justify-end py-2">
                    <button
                      @click="saveSelection"
                      class="bg-blue-600 text-white px-4 py-2 rounded-md hover:bg-blue-700"
                    >
                      Save
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </form>
      </div>
    </section>

    <section class="py-16">
      <div class="container mx-auto px-4">
        <h2 class="text-3xl font-semibold text-gray-800 mb-8">
          Available Hotels
        </h2>
        <div
          class="flex flex-row gap-4 justify-end h-12 items-center bg-white p-6 mb-4"
        >
          <label for="sort">Order by:</label>
          <select class="bg-white" v-model="sortBy">
            <option value="price">Price</option>
            <option value="rating">Ratings</option>
            <option value="name">Name</option>
          </select>
        </div>

        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8">
          <div
            v-for="hotel in filteredHotels"
            :key="hotel.id"
            class="bg-white p-6 rounded-lg shadow-md"
          >
            <img
              :src="hotel.image"
              :alt="hotel.name"
              class="w-full h-48 object-cover rounded-md"
            />
            <h3 class="text-xl font-bold text-gray-800 mt-4">
              {{ hotel.name }}
            </h3>
            <p class="text-gray-600 mt-2">{{ hotel.location }}</p>
            <p class="text-gray-400 mt-2">
              {{ hotel.rating }} <span>stars</span>
            </p>
            <p class="text-blue-500 font-semibold mt-4">
              {{ hotel.price }} /night
            </p>
            <div class="flex">
              <p class="mr-2">Compare hotels</p>
              <input
                type="checkbox"
                :value="hotel"
                @click="toggleHotelSelection(hotel)"
              />
            </div>
            <button
              class="block w-full mt-4 text-center bg-blue-600 text-white py-2 rounded-md hover:bg-blue-700"
              @click="makeReservation(hotel.id)"
            >
              Book Now
            </button>
          </div>
        </div>
      </div>
    </section>
    <div v-if="selectedHotels.length > 1">
      <ComparisonHotelTable
        :hotels="selectedHotels"
        @close="selectedHotels.length = 0"
      />
    </div>

    <HotelBookingModal
      :is-open="openModal"
      :reservation="reservation"
      :book="guests"
      @close="closeModal"
    />

    <footer class="bg-blue-600 py-4">
      <div class="container mx-auto text-center text-white">
        <p>&copy; 2024 HotelFinder. All rights reserved.</p>
      </div>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from "vue";
import type { Hotel, Guests } from "../types/index";

definePageMeta({
  middleware: "auth",
});

const transform = { transform: (_hotels) => _hotels.data };
const { data: hotels } = await useLazyFetch("/api/hotels", transform);

const destination = ref<string>("");
const checkInDate = ref<string>("");
const checkOutDate = ref<string>("");
const selectedHotels = ref<Hotel[]>([]);
const isOpen = ref<boolean>(false);
const adults = ref<number>(1);
const children = ref<number>(0);
const rooms = ref<number>(1);
const sortBy = ref<string>("name");
const openModal = ref<boolean>(false);
const reservation = ref<Hotel | null>(null);
const guests = ref<Guests>({
  rooms: 1,
  adults: 1,
  children: 0,
  checkin: "",
  checkout: "",
});

const filteredHotels = computed(() => {
  if (destination.value) {
    return hotels.value.filter((hotel) =>
      hotel.location.toLowerCase().includes(destination.value.toLowerCase()),
    );
  }

  switch (sortBy.value) {
    case "price":
      return hotels.value.sort((room, hotel) => room.price - hotel.price);
    case "rating":
      return hotels.value.sort((room, hotel) => hotel.rating - room.rating);
    case "name":
      return hotels.value.sort((room, hotel) =>
        room.name.localeCompare(hotel.name),
      );
    default:
      return hotels.value;
  }
});

const toggleHotelSelection = (hotel: Hotel) => {
  const index = selectedHotels.value.findIndex(
    (selected) => selected.id === hotel.id,
  );

  if (index === -1) {
    selectedHotels.value.push(hotel);
  } else {
    selectedHotels.value.splice(index, 1);
  }
};

const toggleDropdown = () => {
  isOpen.value = !isOpen.value;
};

const saveSelection = () => {
  guests.value = {
    rooms: rooms.value,
    adults: adults.value,
    children: children.value,
    checkin: checkInDate.value,
    checkout: checkOutDate.value,
  };
  isOpen.value = false;
};

const makeReservation = (id: number) => {
  openModal.value = true;
  reservation.value = hotels.value.find((hotel) => hotel.id === id) || null;
};

const closeModal = (payload: boolean) => {
  openModal.value = payload;
};
</script>
