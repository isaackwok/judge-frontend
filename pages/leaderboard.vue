<template>
  <form>
    <div
      class="flex flex-col bg-white p-4 md:p-16 md:mt-10 rounded shadow text-left text-gray-700"
    >
      <input
        type="text"
        v-model="searchId"
        name="sid"
        placeholder="Search by studentID ..."
        @input="submit"
        minlength="9"
        maxlength="9"
        class="border shadow rounded p-2"
      />
      <table class="table-auto">
        <thead>
          <tr>
            <th class="p-2 md:p-5">Rank</th>
            <th class="p-2 md:p-5">StudentID</th>
            <th class="p-2 md:p-5">ModelName</th>
            <th class="p-2 md:p-5">Score</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(row, index) in results" :key="index">
            <td class="relative text-center p-2 md:p-5">
              <i
                class="transform -rotate-12 fas fa-crown absolute left-0"
                :class="{
                  'text-orange-400': row[0] === 1,
                  'text-gray-400': row[0] === 2,
                  'text-orange-900': row[0] === 3,
                }"
                v-if="row[0] <= 3"
              >
              </i>
              {{ row[0] }}
            </td>
            <td class="p-2 md:p-5">{{ row[1] }}</td>
            <td class="p-2 md:p-5">{{ row[2] }}</td>
            <td class="p-2 md:p-5">
              {{ (row[3] * 100).toFixed(2) }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      sid: "",
      pwd: "",
      modelName: "",
      searchId: "",
      results: [
        //   [1, "108065402", "Super Classfier Ultra v2", 99.87],
        //   [2, "108065402", "Super Classfier Ultra v2", 99.87],
        //   [3, "108065402", "Super Classfier Ultra v2", 99.87],
        //   [4, "108065402", "Super Classfier Ultra v2", 99.87],
        //   [5, "108065402", "Super Classfier Ultra v2", 99.87],
        //   [6, "108065402", "Super Classfier Ultra v2", 99.87],
      ],
    };
  },
  methods: {
    async submit(e) {
      console.log(this.searchId.length);
      if (this.searchId.length === 9) {
        let formData = new FormData();
        formData.append("sid", this.searchId);
        this.results = await fetch("http://thor.nlplab.cc:11111/personalRank", {
          method: "POST",
          body: formData,
        })
          .then((res) => res.json())
          .then((json) => json.results);
      }
    },
  },
  async fetch() {
    this.results = await fetch("http://thor.nlplab.cc:11111/leaderboard", {
      method: "POST",
    })
      .then((res) => res.json())
      .then((json) => json.results);
    // console.log(response);
  },
};
</script>