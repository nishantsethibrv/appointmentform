<template>
  <form @submit.prevent="handleSubmit" class="max-w-md mx-auto p-6 rounded">
    <h1 class="text-3xl font-bold pb-3">Appointment Form</h1>
    <div class="mb-4">
      <label for="name">Name</label>
      <input
        v-model="formdata.name"
        type="text"
        class="w-full"
        :class="{ 'border-red': errors.name }"
      />
      <p v-if="errors.name" class="text-red-500">{{ errors.name }}</p>
    </div>

    <div class="mb-4">
      <label for="email">Email</label>
      <input
        v-model="formdata.email"
        type="email"
        class="w-full"
        :class="{ 'border-red-500': errors.email }"
      />
      <p v-if="errors.email" class="text-red-500">{{ errors.email }}</p>
    </div>

    <div class="mb-4">
      <label for="phone">Phone</label>
      <input
        v-model="formdata.phone"
        type="tel"
        class="w-full"
        :class="{ 'border-red-500': errors.phone }"
      />
      <p v-if="errors.phone" class="text-red-500">{{ errors.phone }}</p>
    </div>

    <div class="mb-4">
      <label for="timeslot">Time Slot</label>
      <select
        v-model="formdata.timeslot"
        class="w-full"
        :class="{ 'border-red-500': errors.timeslot }"
      >
        <option value="">Select a time slot</option>
        <option v-for="slot in availableslots" :key="slot" :value="slot">
          {{ slot }}
        </option>
      </select>
      <p v-if="errors.timeslot" class="text-red-500">{{ errors.timeslot }}</p>
    </div>

    <button
      type="submit"
      class="w-full py-2 text-white bg-indigo-600 rounded-md"
    >
      Book Appointment
    </button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      formdata: {
        name: "",
        email: "",
        phone: "",
        timeslot: "",
      },
      errors: {},
      availableslots: ["10:00 AM", "11:00 AM", "12:00 PM", "1:00 PM", "2:00 PM"],
      bookedslots: ["10:00 AM"],
    };
  },
  methods: {
    validateForm() {
      this.errors = {};

      if (!this.formdata.name) {
        this.errors.name = "Name is required.";
      }

      if (!this.formdata.email || !/^\S+@\S+\.\S+$/.test(this.formdata.email)) {
        this.errors.email = "A valid email address is required.";
      }

      if (!this.formdata.phone || !/^\d{10}$/.test(this.formdata.phone)) {
        this.errors.phone = "A valid 10-digit phone number is required.";
      }

      if (!this.formdata.timeslot) {
        this.errors.timeslot = "Please select a time slot.";
      } else if (this.bookedslots.includes(this.formdata.timeslot)) {
        this.errors.timeslot = "This time slot is already booked.";
      }

      return Object.keys(this.errors).length === 0;
    },
    handleSubmit() {
      if (this.validateForm()) {
        alert("its booked now");
      }
    },
  },
};
</script>
