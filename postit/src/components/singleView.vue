<template>
  <div>
    <button
      class="me-3 inline-block rounded bg-primary px-6 pb-2 pt-2.5 text-xs font-medium uppercase leading-normal text-white shadow-primary-3 transition duration-150 ease-in-out hover:bg-primary-accent-300 hover:shadow-primary-2 focus:bg-primary-accent-300 focus:shadow-primary-2 focus:outline-none focus:ring-0 active:bg-primary-600 active:shadow-primary-2 motion-reduce:transition-none dark:shadow-black/30 dark:hover:shadow-dark-strong dark:focus:shadow-dark-strong dark:active:shadow-dark-strong absolute top-30 left-10"
      @click="$router.push('/')"
    >
      RETOUR
    </button>
    <ul>
      <li class="justify-center">
        <a
          title="Cliquez pour éditer le contenu"
          href="#"
          class="no-underline color-black bg-yellow-100 block w-500 px-1 py-1 shadow-xl mt-20 detail max-w-90%"
        >
          <h2 contenteditable="true" class="title">{{ title }}</h2>
          <p class="w-100% mb-10 single" contenteditable="true">
            {{ content }}
          </p>
          <button
            class="me-3 inline-block rounded bg-primary px-6 pb-2 pt-2.5 text-xs font-medium uppercase leading-normal text-white shadow-primary-3 transition duration-150 ease-in-out hover:bg-primary-accent-300 hover:shadow-primary-2 focus:bg-primary-accent-300 focus:shadow-primary-2 focus:outline-none focus:ring-0 active:bg-primary-600 active:shadow-primary-2 motion-reduce:transition-none dark:shadow-black/30 dark:hover:shadow-dark-strong dark:focus:shadow-dark-strong dark:active:shadow-dark-strong absolute bottom-1 right-5"
            @click="update(id)"
          >
            Valider
          </button>
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "singleView",
  data() {
    return {
      id: "",
      title: "",
      content: [],
      Resp: "",
    };
  },
  mounted() {
    this.getData(this.$route.params.id);
  },
  methods: {
    getData(param) {
      var requestOptions = {
        method: "GET",
        redirect: "follow",
      };

      fetch(`https://post-it.epi-bluelock.bj/notes/${param}`, requestOptions)
        .then((response) => response.json())
        .then((result) => {
          this.id = result._id;
          this.title = result.title;
          this.content = result["content"][0];
        })
        .catch((error) => console.log("error", error));
    },
    update(param) {
      let titleUpdate = document.querySelector("h2").textContent;
      let contentUpdate = document.querySelector("p").textContent;
      // const element = document.querySelector("#put-request .date-updated");
      const requestOptions = {
        method: "PUT",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ title: titleUpdate, content: [contentUpdate] }),
      };
      fetch(
        `https://post-it.epi-bluelock.bj/notes/${param}`,
        requestOptions
      ).then((response) => {
        response.json(), (this.Resp = response["status"]), this.message();
      });
      console.log(this.Resp);
    },
    message() {
      if (this.Resp == "200") {
        window.location.replace("/");
      }
    },
  },
};
</script>
