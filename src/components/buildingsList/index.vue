<template>
  <div>
    <div class="main_container">
      <table border="2px">
        <th>Номер будинку</th>
        <tr v-for="(buildingNumber, index) in paginatedUsers" :key="index">
          <td
            :class="{
              valid_row: checkRow(buildingNumber),
              invalid_row: !checkRow(buildingNumber),
            }"
          >
            {{ buildingNumber }}
          </td>
        </tr>
      </table>
    </div>
    <div class="pagination_container">
      <div
        class="page"
        v-for="(page, index) in pages"
        :key="page"
        @click="onPageClick(page)"
        :class="{
          selected_item: isCurrentIndex(index),
        }"
      >
        {{ page }}
      </div>
    </div>
  </div>
</template>

<script>
import buildingNumbers from "!raw-loader!@/assets/buildingNumbers.txt";
export default {
  name: "buildingsList",
  data() {
    return {
      buildingNumbersArray: [],

      buildingNumbersPerPage: 1000,

      pageNumber: 1,
    };
  },
  computed: {
    pages() {
      return Math.ceil(this.buildingNumbersArray.length / 1000);
    },

    paginatedUsers() {
      let from = (this.pageNumber - 1) * this.buildingNumbersPerPage;
      let to = from + this.buildingNumbersPerPage;
      return this.buildingNumbersArray.slice(from, to);
    },
  },

  methods: {
    onPageClick(page) {
      this.pageNumber = page;
    },

    isCurrentIndex(index) {
      return index + 1 === this.pageNumber;
    },

    checkRow(buildingNumber) {
      const pattern =
        /^[1-9]\d{0,2}[a-eа-дA-EА-Д]?([\-\/][1-9]?\d{0,2}?[a-eа-дA-EА-Д]?)?$/gm; //eslint-disable-line

      const regExp = new RegExp(pattern);
      if (regExp.test(buildingNumber) == true) {
        return true;
      } else return false;
    },
  },

  mounted() {
    let file = buildingNumbers;
    let reader = new FileReader();
    let data = new Blob([file]);
    reader.readAsText(data);
    reader.onload = (res) => {
      this.buildingNumbersArray = res.target.result.split("\n");
    };
  },
};
</script>

<style lang="scss" scoped>
.main_container {
  table {
    margin: 0 auto;
  }
}

.pagination_container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  .page {
    padding: 6px;
    border: solid 3px #e7e7e7;
    margin-right: 5px;
    &:hover {
      background: #aeaeae;
      cursor: pointer;
    }
  }
}

.selected_item {
  background: forestgreen;
  color: #fff;
}

.valid_row {
  background-color: rgba(33, 207, 33, 0.459);
}

.invalid_row {
  background-color: rgba(204, 49, 49, 0.521);
}
</style>
