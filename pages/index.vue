<template>
  <main class="h-screen bg-gray-100 pt-12">
    <div class="container mx-auto max-w-4xl px-4">
      <h1 class="text-3xl text-gray-700 font-bold">Contact Us</h1>
      <div class="border-b-4  my-8"></div>
      <form @submit.prevent="send">
        <div class="flex flex-wrap mb-6 -mx-4">
          <div class="w-full md:w-1/2 mb-6 md:mb-0 px-4">
            <label for="name" class="block mb-2 text-gray-600 font-bold"
              >Name</label
            >
            <input
              name="name"
              id="name"
              v-model="form_data.name"
              placeholder="Jon Snow"
              required="required"
              class="block w-full shadow rounded outline-none mb-2 p-4"
              type="text"
            />
          </div>
          <div class="w-full px-4 md:w-1/2">
            <label for="email" class="block text-gray-600 font-bold mb-2"
              >Email Address</label
            >
            <input
              type="email"
              name="email"
              id="email"
              v-model="form_data.email"
              placeholder="email@example.com"
              required="required"
              class="block w-full shadow rounded outline-none mb-2 p-4"
            />
          </div>
        </div>
        <div class="flex flex-wrap mb-6 -mx-4">
          <div class="w-full md:w-1/2 mb-6 md:mb-0 px-4">
            <label for="order" class="block mb-2 text-gray-600 font-bold"
              >Order Number</label
            >
            <input
              name="order"
              id="order"
              v-model="form_data.order"
              placeholder="ABC1244"
              required="required"
              class="block w-full shadow rounded outline-none mb-2 p-4"
              type="text"
            />
          </div>
          <div class="w-full px-4 md:w-1/2">
            <label for="email" class="block text-gray-600 font-bold mb-2"
              >Complaint type</label
            >
            <div class="relative">
              <select
                required
                v-model="form_data.complaint"
                class="block bg-white shadow rounded appearance-none w-full p-4 pr-8 rounded outline-none"
                id="grid-state"
              >
                <option selected disabled value="">Select</option>
                <option value="Order related">Order related</option>
                <option value="Payment related">Payment related</option>
                <option value="Account related">Account related</option>
                <option value="Others">Others</option>
              </select>
              <div
                class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700"
              >
                <svg
                  class="fill-current h-4 w-4"
                  xmlns="http://www.w3.org/2000/svg"
                  viewBox="0 0 20 20"
                >
                  <path
                    d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"
                  />
                </svg>
              </div>
            </div>
          </div>
        </div>

        <div class="flex flex-wrap mb-6 -mx-4">
          <div class="w-full px-4">
            <label for="message" class="block mb-2 text-gray-600 font-bold"
              >Message</label
            >
            <textarea
              name="message"
              id="message"
              rows="4"
              v-model="form_data.message"
              placeholder="Enter your query/complaint here"
              required="required"
              class="block w-full shadow rounded outline-none mb-2 p-4"
              type="text"
            />
          </div>
        </div>
        <div>
          <button
            :disabled="loading"
            class="bg-indigo-500 text-white px-8 py-4 uppercase font-bold rounded shadow"
          >
            {{ btnLabel }}
          </button>
        </div>
      </form>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      btnLabel: "Submit",
      loading: false,
      form_data: {
        name: "",
        email: "",
        order: "",
        complaint: "",
        message: ""
      }
    };
  },
  methods: {
    async send() {
      try {
        this.btnLabel = "Submitting, hold tight!";
        this.loading = true;
        const { data } = await this.$axios.post(
          "https://telegram-bot-example.glitch.me/send-message",
          this.form_data
        );
        this.$toast.success("Message sent succesfully", {
          position: "bottom-center",
          duration: 5000
        });
        this.loading = false;
        this.btnLabel = "Submit";
      } catch (err) {
        this.btnLabel = "Submit";
        this.loading = false;
        this.$toast.success("Message sending failed");
      }
    }
  }
};
</script>

<style></style>
