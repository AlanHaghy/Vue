<script>
import Cards from "./components/Cards/Cards.vue";

export default {
  name: "app",
  components: { Cards },
  data: () => ({
    cards: [
      {
        title: "Writer & Publisher",
        priceTag: 0,
        nonRefundable: false,
        caption:
          "ASCAP royalties are split evently between writes and publishers. Join as both to ensure you get paid everything you deserve.",
        isError: false,
        selected: false,
        requirements: [
          "Legal Name",
          "Mailing address",
          "Valid Email Address",
          "SSN/ITIN",
          "Must be 18 or older to apply online*",
        ],
      },
      {
        title: "Writer",
        priceTag: 0,
        nonRefundable: false,
        caption:
          "Writers create musical compositions: the melody, harmoney, lyrics, beats arrangements, etc.",
        isError: false,
        selected: false,
        requirements: [
          "Legal Name",
          "Mailing address",
          "Valid Email Address",
          "SSN/ITIN",
          "Must be 18 or older to apply online*",
        ],
      },
      {
        title: "Publisher",
        priceTag: 50,
        nonRefundable: true,
        caption:
          "Publishers handle the business side of musical compositions, like licensing and copyright administration.",
        isError: false,
        selected: false,
        requirements: [
          "Legal Name",
          "Mailing address",
          "Valid Email Address",
          "SSN/ITIN",
          "Must be 18 or older to apply online*",
        ],
      },
    ],
    selectList: [
      "individual / Sole Propriotor or Single-member LLC",
      "C Corporation",
      "S Corporation",
      "LLC-C Corporation",
      "LLC-S Corporation",
      "LLC Partnership",
    ],
    showError: false,
    showList: false,
    showErrorList: false,
    selectedOption: "",
    selectedCategory: {
      card: "",
      pubType: "",
    },
  }),
  methods: {
    submitBtn() {
      if (this.showList) {
        this.selectedCategory.pubType = this.selectedOption;
        console.log(this.selectedCategory);
        if (this.selectedOption == "") {
          this.showErrorList = true;
          console.log("error");
        } else {
          this.showErrorList = false;
        }
      }

      if (this.selectedCategory.card === "") {
        this.cards.forEach((card) => {
          card.isError = true;
        });
        this.showError = true;
      } else {
        this.showList = true;
      }
    },
    handleClick(cardName, event) {
      if (event) {
        event.preventDefault();
      }
      this.cards.forEach((card) => {
        if (card.title === cardName) {
          card.selected = true;
          this.selectedCategory.card = card.title;
        } else {
          card.selected = false;
        }
        card.isError = false;
      });
      this.showError = false;
    },
  },
};
</script>

<template>
  <div class="headerLabel">Choose member type</div>
  <div class="cardHolder">
    <span v-for="card in cards" :key="card.title">
      <Cards
        @click="handleClick(card.title, $event)"
        :title="card.title"
        :price-tag="card.priceTag"
        :non-refundable="card.nonRefundable"
        :is-error="card.isError"
        :selected="card.selected"
        :caption="card.caption"
        :req="card.requirements"
    /></span>
  </div>
  <div class="warning" v-show="showError">
    Please select your membership type!
  </div>

  <div class="selector" v-show="showList">
    <label class="headerLabel"
      >Publisher Company Type</label>
      <div class="subtitle">Please select the federal tax classification of your publisher
        company.</div>

    <select :class="['dropdown',{dropwanr : showErrorList}]" v-model="selectedOption">
      <option disabled value="">Publisher Company type</option>
      <option v-for="option in selectList" :key="option" :value="option">
        {{ option }}
      </option>
    </select>
    <div class="warning" v-show="showErrorList">Please select your publisher company type</div>
  </div>

  <div>
    <button @click="submitBtn">{{ showList ? "Continue" : "Next" }}</button>
  </div>
</template>

<style scoped>
@import "./assets/style.scss";
</style>
