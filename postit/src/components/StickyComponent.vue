<!-- eslint-disable vue/no-parsing-error -->
<!-- eslint-disable vue/require-v-for-key -->
<template>
  <div>
    <div class="alert">{{ msg }}</div>
    <ul>
      <li v-for="post in notes">
        <a
          href="#"
          class="no-underline color-black bg-yellow-100 block h-20% max-w-200 px-1 py-1 shadow-xl mt-10"
        >
          <h2 contenteditable="false">{{ post["title"] }}</h2>
          <p class="line-clamp-5 max-h-200" contenteditable="false">
            {{ post["content"][0] }}
          </p>
          <button
            class="me-3 inline-block rounded bg-primary px-6 pb-2 pt-2.5 text-xs font-medium uppercase leading-normal text-white shadow-primary-3 transition duration-150 ease-in-out hover:bg-primary-accent-300 hover:shadow-primary-2 focus:bg-primary-accent-300 focus:shadow-primary-2 focus:outline-none focus:ring-0 active:bg-primary-600 active:shadow-primary-2 motion-reduce:transition-none dark:shadow-black/30 dark:hover:shadow-dark-strong dark:focus:shadow-dark-strong dark:active:shadow-dark-strong mt-20 absolute bottom-3 left-5"
            @click="deleteNote(post._id)"
          >
            Supprimer
          </button>
          <button
            class="me-3 inline-block rounded bg-primary px-6 pb-2 pt-2.5 text-xs font-medium uppercase leading-normal text-white shadow-primary-3 transition duration-150 ease-in-out hover:bg-primary-accent-300 hover:shadow-primary-2 focus:bg-primary-accent-300 focus:shadow-primary-2 focus:outline-none focus:ring-0 active:bg-primary-600 active:shadow-primary-2 motion-reduce:transition-none dark:shadow-black/30 dark:hover:shadow-dark-strong dark:focus:shadow-dark-strong dark:active:shadow-dark-strong absolute bottom-3 right-5"
            @click="$router.push('/detail/' + post._id)"
          >
            VOIR PLUS...
          </button>
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      notes: [],
      // eslint-disable-next-line vue/no-dupe-keys
      msg: "",
      Resp: "",
    };
  },
  mounted() {
    this.getData();
  },
  methods: {
    getData() {
      var requestOptions = {
        method: "GET",
        redirect: "follow",
      };

      fetch("https://post-it.epi-bluelock.bj/notes/", requestOptions)
        .then((response) => response.json())
        .then((result) => (this.notes = result.notes))
        .catch((error) => console.log("error", error));
    },
    deleteNote(param) {
      var requestOptions = {
        method: "DELETE",
        redirect: "follow",
      };
      fetch(
        `https://post-it.epi-bluelock.bj/notes/${param}`,
        requestOptions
      ).then((response) => {
        response.json(), (this.Resp = response["status"]), this.message();
      });
      // .catch((error) => console.log("error", error));
    },
    message() {
      if (this.Resp == "200") {
        this.getData();
        this.msg = "Supprimé avec succès";
        document.querySelector(".alert").textContent = this.msg;
        setTimeout(function () {
          this.msg = " ";
          document.querySelector(".alert").textContent = "";
        }, 2000);
      }
    },
  },
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Sticky",
};
</script>
