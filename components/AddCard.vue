<template>
  <div class="left-bar">
    <div class="required">Наименование товара <span></span></div>
    <input
      type="text"
      name="title"
      v-model="title"
      v-bind:class="[isTitleEmpty ? emptyClass : unemptyClass]"
      placeholder="Введите наименование товара"
    />

    <div>Описание товара</div>
    <textarea
      class="description-product"
      name="descrip"
      v-model="descrip"
      v-on:input="
        validation($event.target.name);
        handlyInput;
      "
      type="text"
      placeholder="Введите описание товара"
    ></textarea>

    <div class="required">Ссылка на изображение товара <span></span></div>
    <input
      type="text"
      name="link"
      v-model="link"
      v-on:input="validation($event.target.name)"
      v-bind:class="[isLinkEmpty ? emptyClass : unemptyClass]"
      placeholder="Введите ссылку"
    />

    <div class="required">Цена товара <span></span></div>
    <input
      type="text"
      class="price-product"
      name="price"
      v-model="price"
      v-on:input="
        validation($event.target.name);
        handlyInput;
      "
      v-bind:class="[isPriceEmpty ? emptyClass : unemptyClass]"
      placeholder="Введите цену"
    />
    <button
      id="add-btn"
      :disabled="disabledBtn"
      v-bind:class="[isBtnActive ? activeClass : unactiveClass]"
      v-on:click="addCard"
    >
      Добавить товар
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      isTitleEmpty: false,
      descrip: "",
      link: "",
      isLinkEmpty: false,
      price: "",
      isPriceEmpty: false,
      emptyClass: "empty",
      unemptyClass: "unempty",
      isBtnActive: false,
      activeClass: "active",
      unactiveClass: "unactive",
      disabledBtn: true,
      needDoList: [],
    };
  },
  methods: {
    validation(name) {
      if (name == "price") {
        this.price = this.price.replace(/\s/g, "");
        this.price = this.price.replace(/(\d)(?=(\d{3})+(\D|$))/g, "$1 ");
      }
      if (name == "title" || name == "link" || name == "price") {
        if (this.title !== "" && this.link !== "" && this.price !== "") {
          this.disabledBtn = false;
          this.isBtnActive = true;
          this.checkInput();
        } else {
          this.checkInput();
        }
      }
    },
    checkInput() {
      this.isTitleEmpty = this.title == "";
      this.isLinkEmpty = this.link == "";
      this.isPriceEmpty = this.price == "";
    },
    handlyInput(event) {
      this.title = event.target.value;
      this.descrip = event.target.value;
      this.link = event.target.value;
      this.price = event.target.value;
    },
    addCard() {
      this.$parent.addCard(this);
      this.$parent.saveCards(this);
    },
    haveList() {
      this.$parent.haveList(this);
    },
  },
};
</script>

<style lang="scss">
.left-bar {
  max-width: 284px;
  max-height: 392px;
  padding: 24px;
  background-color: #ffffff;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 5px;
  margin-right: 16px;
  div {
    width: 284px;
    margin: 0;
    font-size: 10px;
    margin-bottom: 4px;
  }
  input {
    width: 252px;
    height: 16px;
    font-size: 12px;
    padding: 10px 16px;
    margin-bottom: 16px;
    border-radius: 5px;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  }
  button {
    width: 284px;
    height: 36px;
    border: none;
    font-size: 12px;
    cursor: pointer;
    border-radius: 10px;
  }
}
.description-product {
  height: 108px;
  width: 252px;
  font-size: 12px;
  padding: 10px 16px;
  border: none;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
}
.price-product {
  font-weight: 600;
}
.empty {
  border: 2px solid #ff8484;
}
.unempty {
  border: 2px solid transparent;
}
.active {
  color: white;
  background: #7bae73;
}
.unactive {
  color: #b4b4b4;
  background: #eeeeee;
}
.required {
  display: block;
  position: relative;
  span {
    position: absolute;
    top: 0;
    width: 4px;
    height: 4px;
    border-radius: 50%;
    background-color: #ff8484;
  }
}
</style>
