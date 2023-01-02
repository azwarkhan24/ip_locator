<template>
  <div>
    <!-- navbar -->
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <h3 class="mx-auto text-white">
        <i class="fa-solid fa-earth-asia me-3"></i>IP LOCATOR
      </h3>
      <button type="button" class="btn btn-warning me-3">signup</button>
    </nav>
    <!-- Logo -->

    <!-- input -->
    <div class="input-control d-flex">
      <input
        placeholder="Enter IP Address"
        ref="anyName"
        v-model="query"
        @keypress="
          fetchData();
          resetResult();
        "
      />
      <i
        class="fa-solid fa-circle-xmark icon"
        @click="
          resetInput();
          resetiInput();
        "
      ></i>
    </div>
    <!-- data -->
   <div class="d-flex  ">
    <div class="list-group" v-if="showText">
      <a href="#" class="list-group-item list-group-item-action d-flex"
        ><h6 class="">status:</h6>
        <p class="ms-3">"{{ tracker.status }}"</p></a
      >
      <a href="#" class="list-group-item list-group-item-action d-flex"
        ><h6 class="">country:</h6>
        <p class="ms-3">"{{ tracker.country }}"</p></a
      >
      <a href="#" class="list-group-item list-group-item-action d-flex"
        ><h6 class="">country code:</h6>
        <p class="ms-3">"{{ tracker.countryCode }}"</p></a
      >
      <a href="#" class="list-group-item list-group-item-action d-flex"
        ><h6 class="">region:</h6>
        <p class="ms-3">"{{ tracker.region }}"</p></a
      >
      <a href="#" class="list-group-item list-group-item-action d-flex"
        ><h6 class="">city:</h6>
        <p class="ms-3">"{{ tracker.city }}"</p></a
      >
      <a href="#" class="list-group-item list-group-item-action d-flex"
        ><h6 class="">zip:</h6>
        <p class="ms-3">"{{ tracker.zip }}"</p></a
      >
      <a href="#" class="list-group-item list-group-item-action d-flex"
        ><h6 class="">lat:</h6>
        <p class="ms-3">"{{ tracker.lat }}"</p></a
      >
      <a href="#" class="list-group-item list-group-item-action d-flex"
        ><h6 class="">lon:</h6>
        <p class="ms-3">"{{ tracker.lon }}"</p></a
      >
      <a href="#" class="list-group-item list-group-item-action d-flex"
        ><h6 class="">timezone:</h6>
        <p class="ms-3">"{{ tracker.timezone }}"</p></a
      >
    </div>
    <div>
      <h3 class="mt-5 map">Map Location</h3>
      <iframe
      class="map"
        width="300"
        height="170"
        frameborder="0"
        scrolling="no"
        marginheight="0"
        marginwidth="0"
        :src="
          'https://maps.google.com/maps?q=' +
          tracker.lat +
          ',' +
          tracker.lon +
          '&hl=es&z=14&amp;output=embed'
        "
      >
      </iframe>
    </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ipTracker",
  data() {
    return {
      showText: false,
      query: "",
      tracker: {},
    };
  },
  methods: {
    fetchData() {
      fetch(`http://ip-api.com/json/${this.query}`)
        .then((response) => {
          return response.json();
        })
        .then(this.setResults);
    },
    setResults(results) {
      this.tracker = results;
      console.log(this.tracker);
    },
    resetInput() {
      this.query = "";
    },
    resetResult() {
      this.showText = true;
    },
    resetiInput() {
      this.showText = false;
    },
  },
};
</script>

<style>
.input-control {
  display: flex;
  flex-direction: column;
  margin-left: 50px;
}

.input-control input {
  border: 2px solid rgb(233, 231, 231);
  border-radius: 6px;

  font-size: 12px;
  padding: 10px;
  width: 30%;
  background-color: rgb(233, 231, 231);
  color: black;
  margin-left: 50px;
  margin-top: 25px;
}

.input-control input:focus {
  outline: 0;
}
.icon {
  margin-left: 420px;
  margin-top: -30px;
  cursor: pointer;
}

.list-group {
  width: 29%;
  margin-top: 20px;
  margin-left: 100px;
}
.map{
  margin-left: 400px;
}
</style>
