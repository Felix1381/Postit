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
          class="no-underline color-black bg-yellow-100 block px-1 py-1 shadow-xl mt-20 detail"
        >
          <h2
            data-placeholder="Cliquez pour insérer le titre..."
            contenteditable="true"
            class="title"
          ></h2>
          <p
            class="w-100% mb-10 single"
            data-placeholder="Cliquez pour insérer le contenu..."
            contenteditable
          >
            {{ content[0] }}
          </p>
          <button
            class="me-3 inline-block rounded bg-primary px-6 pb-2 pt-2.5 text-xs font-medium uppercase leading-normal text-white shadow-primary-3 transition duration-150 ease-in-out hover:bg-primary-accent-300 hover:shadow-primary-2 focus:bg-primary-accent-300 focus:shadow-primary-2 focus:outline-none focus:ring-0 active:bg-primary-600 active:shadow-primary-2 motion-reduce:transition-none dark:shadow-black/30 dark:hover:shadow-dark-strong dark:focus:shadow-dark-strong dark:active:shadow-dark-strong absolute bottom-1 left-5"
            @click="$router.push('/')"
          >
            ANNULER
          </button>
          <button
            class="me-3 inline-block rounded bg-primary px-6 pb-2 pt-2.5 text-xs font-medium uppercase leading-normal text-white shadow-primary-3 transition duration-150 ease-in-out hover:bg-primary-accent-300 hover:shadow-primary-2 focus:bg-primary-accent-300 focus:shadow-primary-2 focus:outline-none focus:ring-0 active:bg-primary-600 active:shadow-primary-2 motion-reduce:transition-none dark:shadow-black/30 dark:hover:shadow-dark-strong dark:focus:shadow-dark-strong dark:active:shadow-dark-strong absolute bottom-1 right-5"
            @click="update()"
          >
            CREER
          </button>
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "createPost",
  data() {
    return {
      id: "",
      title: "",
      content: [],
      Resp: "",
    };
  },
  methods: {
    update() {
      let titleUpdate = document.querySelector("h2").textContent;
      let contentUpdate = document.querySelector("p").textContent;
      const requestOptions = {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ title: titleUpdate, content: [contentUpdate] }),
      };
      fetch(`https://post-it.epi-bluelock.bj/notes/`, requestOptions).then(
        (response) => {
          response.json(), (this.Resp = response["status"]), this.message();
        }
      );
    },
    message() {
      if (this.Resp == "201") {
        window.location.replace("/");
      }
    },
  },
};
</script>
