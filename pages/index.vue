<template>
  <form
    @submit="submit"
    method="POST"
    action="http://thor.nlplab.cc:11111/scorer"
  >
    <div
      class="flex flex-col bg-white p-4 md:p-24 md:mt-10 rounded shadow text-left text-gray-700"
    >
      <p class="mt-0 required">Student ID:</p>
      <input
        v-model="sid"
        placeholder="108065402"
        class="rounded shadow p-2 border"
        type="text"
        name="sid"
        maxlength="9"
        minlength="9"
        required
      />
      <p class="required">Password:</p>
      <input
        placeholder="AbCdEfG123"
        v-model="pwd"
        class="rounded shadow p-2 border"
        type="password"
        name="pwd"
        autocomplete="current-passsword"
        required
      />
      <p class="required">Upload Model (ex. 108065402.pickle):</p>
      <input
        class="rounded shadow bg-white p-2 border"
        type="file"
        name="file"
        id="file"
        required
      />
      <p>Model name:</p>
      <p class="text-gray-500 text-sm mt-0 italic">
        Name your model with an awesome name !!! Default is your student ID.
      </p>
      <input
        v-model="modelName"
        placeholder="Super Classifier v2 Ultra"
        class="rounded shadow p-2 border"
        type="text"
        name="modelName"
        maxlength="30"
      />
      <input
        type="submit"
        value="Submit"
        class="v-bg-green p-3 rounded shadow mt-10 text-white"
      />
    </div>
  </form>
</template>

<script>
// eruo0ntXgO
export default {
  data() {
    return {
      sid: "",
      pwd: "",
      modelName: "",
    };
  },
  methods: {
    async submit(e) {
      e.preventDefault();
      let file = document.querySelector("#file");
      let formData = new FormData();
      formData.append("sid", this.sid);
      formData.append("pwd", this.pwd);
      formData.append("modelName", this.modelName || this.sid);
      formData.append("model", file.files[0]);
      fetch("http://thor.nlplab.cc:11111/scorer", {
        method: "POST",
        body: formData,
        headers: {},
      })
        .then((res) => {
          if (res.status === 200) return res.json();
          else throw res;
        })
        .catch((error) => {
          if (error.status === 413)
            alert("Model file too large, should be less than 16MB.");
        })
        .then((json) => {
          alert(
            `The score of model ${this.modelName} is: ${(json.results * 100).toFixed(
              2
            )}`
          );
          window.location.replace("/leaderboard");
        });

      // console.log(response);
    },
  },
};
</script>