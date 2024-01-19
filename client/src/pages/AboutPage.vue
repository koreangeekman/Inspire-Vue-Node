<template>
  <div class="container-fluid">
    <section class="row justify-content-center p-4 pt-5">
      <div class="col-auto d-flex flex-column justify-content-center align-items-center rounded bgBlur py-2 px-3">
        <p class="fs-1 p-2 mb-1 fw-bold">Inspire</p>
        <p class="fs-5 p-2 text-center">
          Create and manage your To-Do list with <br>
          random backgrounds & inspirational quotes!
        </p>
        <div class="">
          <p class="fs-5 p-2 mb-0">
            Additional information by hovering over:
          </p>
          <ul>
            <li style="list-style-type: none ">
              <ul>
                <li>
                  Background Image refresh button
                </li>
              </ul>
              <ul>
                <li>
                  Inspirational Quote
                </li>
              </ul>
              <ul>
                <li>
                  Temperature information
                </li>
              </ul>
            </li>
          </ul>
        </div>
        <p class="fs-5 p-2 m-2 text-center">
          Click the Temperature Widget to swap between ºC & ºF <br>
          Refresh to get the latest weather conditions for Boise,ID <br>
          (<i>Minimum 12 min between polls for weather information</i>) <br>
        </p>
        <p class="fs-5 p-2 m-2 text-center">
          Click the Time Widget to swap between 12 & 24 hour formats <br>
        </p>
        <p class="fs-5 p-2 m-2 text-center">
          Click the Background Image Widget to request a new background <br>
        </p>
        <p class="fs-5 p-2 m-2 text-center">
          Full Stack Application <br>
        </p>
        <p class="fs-5 p-2 m-2 text-center">
          MongoDB, Mongoose ODM, Node.js & Express.js<br>
          HTML, CSS, Bootstrap, JavaScript & Vue.js
        </p>
        <p class="p-2 m-2 text-center">
          - Weather info pulled from the <a href="https://openweathermap.org/" target="_blank">OpenWeather</a> API - <br>
          - Background Image & Quote pulled from
          <a href="https://boisecodeworks.com/" target="_blank">Boise Codeworks'</a> Sandbox -
        </p>
      </div>
    </section>
    <section v-if="authors.length > 0" class="row justify-content-evenly align-items-center flex-column">
      <div class="col-12 d-flex justify-content-center">
        <p class="fs-3 py-2 px-4 mt-3 mb-5 bgBlur rounded text-center">
          Like the app? <br>
          Find out more about the creator below!
        </p>
      </div>
      <div v-for="author in authors" :key="author.email" class="col-12 col-md-6 mb-5 px-4 text-center text-light">
        <UserCard :profile="author" />
      </div>
    </section>
  </div>
</template>

<script>
import { AppState } from "../AppState.js";
import { computed, onMounted } from "vue";
import { accountService } from "../services/AccountService.js";
import UserCard from "../components/UserCard.vue";
import Pop from "../utils/Pop.js";

export default {
  setup() {

    async function _getAppAuthors() {
      try {
        await accountService.getAppAuthors();
      } catch (error) {
        Pop.error(error);
      }
    }

    onMounted(() => {
      if (AppState.authors.length == 0) {
        _getAppAuthors();
      }
    })

    return {
      authors: computed(() => AppState.authors)

    };
  },
  components: { UserCard }
}
</script>


<style lang="scss" scoped>
// hr {
//   margin: 0.5rem;
//   color: #ffffff;
//   box-shadow: 0 0 5px 5px white;
// }

a {
  color: orange;
}

a:hover {
  color: rgb(255, 210, 125);
}

.bgBlur {
  backdrop-filter: blur(5px);
  background-color: #123456b9;
  color: whitesmoke;
}
</style>