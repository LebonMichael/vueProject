<template>
  <div id="nav">
    <router-link class="m-2" :to="{ name: 'TicketDetails', params: { id } }"
      >Details
    </router-link>
    <router-link class="m-2" :to="{ name: 'TicketEdit', params: { id } }">
      Edit
    </router-link>
    <router-link class="m-2" :to="{ name: 'TicketRegister', params: { id } }">
      Register
    </router-link>
    <router-view :event="event"></router-view>
  </div>
</template>

<script>
import TicketService from "@/services/TicketService";

export default {
  name: "TicketDetails",
  props: ["id"],
  data() {
    return {
      event: null,
    };
  },

  created() {
    TicketService.getEvent(this.id)
      .then((response) => {
        this.event = response.data;
        console.log(this.event);
      })
      .catch((error) => {
        console.log(error);
        this.$router.push({
          name: "404Resource",
          params: { resource: "event" },
        });
      });
  },
};
</script>

<style scoped></style>
