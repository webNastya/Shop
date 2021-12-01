<template>
  <div class="container">
    <AddCard />

    <div class="container-goods">
      <div
        class="card"
        v-for="(mask, index) in needDoList"
        :id="mask.id"
        :key="mask.id"
      >
        <div class="basket" v-on:click="removeCard(index)">
          <img src="basket.png" alt="basket" />
        </div>
        <Card :mask="mask" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      card: {
        title: "Наименование товара",
        descrip:
          "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
        link: "card.png",
        price: "10 000",
        id: 0,
      },
      needDoList: [],
      selected: "",
    };
  },
  methods: {
    preprocessor() {
      let localNeedDoList = JSON.parse(localStorage.getItem("cards"));
      if (localNeedDoList != null) this.needDoList = localNeedDoList;
      for (let i = 0; i < 10; i++) {
        let card = { ...this.card };
        card.id = Math.random().toString().slice(2, 11);
        this.needDoList.push(card);
      }
    },
    removeCard(index) {
      this.needDoList.splice(index, 1);

      //Delete in localStorage
      let localNeedDoList = JSON.parse(localStorage.getItem("cards"));
      localNeedDoList.splice(index, 1);
      let data = JSON.stringify(localNeedDoList);
      localStorage.setItem("cards", data);
    },
    addCard(newCarData) {
      let card = {
        title: newCarData.title,
        descrip: newCarData.descrip,
        link: newCarData.link,
        price: newCarData.price,
        id: Math.random().toString().slice(2, 11),
      };

      this.needDoList.unshift(card);

      //Save to localStorage
      if (localStorage.getItem("cards") === null) {
        let data = JSON.stringify(this.needDoList);
        localStorage.setItem("cards", data);
      } else {
        let localNeedDoList = JSON.parse(localStorage.getItem("cards"));
        localNeedDoList.unshift(card);
        let data = JSON.stringify(localNeedDoList);
        localStorage.setItem("cards", data);
      }

      newCarData.title = "";
      newCarData.descrip = "";
      newCarData.link = "";
      newCarData.price = "";
      newCarData.disabledBtn = true;
      newCarData.isBtnActive = false;

      this.sort(this.selected);
    },
    saveCards() {},
    sort(selected) {
      if (selected == "max") {
        this.needDoList.sort((a, b) => {
          let aprice = +a.price.replace(/\s/g, "");
          let bprice = +b.price.replace(/\s/g, "");
          if (bprice > aprice) {
            return 1;
          } else return -1;
        });
      } else if (selected == "min") {
        this.needDoList.sort((a, b) => {
          let aprice = +a.price.replace(/\s/g, "");
          let bprice = +b.price.replace(/\s/g, "");
          if (bprice < aprice) {
            return 1;
          } else return -1;
        });
      } else if (selected == "name") {
        this.needDoList.sort((a, b) => {
          if (b.title.toLowerCase() < a.title.toLowerCase()) {
            return 1;
          } else return -1;
        });
      } else {
        return this.needDoList;
      }
      this.selected = selected;
    },
  },
  created: function () {
    this.preprocessor();
  },
};
</script>

<style lang="scss">
.container-goods {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}
.card {
  max-width: 332px;
  background-color: #ffffff;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 5px;
  margin-bottom: 16px;
  -webkit-border-radius: 5px;
  -moz-border-radius: 5px;
  -ms-border-radius: 5px;
  -o-border-radius: 5px;
  cursor: pointer;
  img {
    max-width: 332px;
    max-height: 200px;
  }
  &:hover {
    .basket {
      transition: transform 0.6s ease;
      display: block;
    }
  }
}
.title-card {
  font-weight: 600;
  margin-bottom: 16px;
}
.description {
  margin-bottom: 32px;
}
.basket {
  width: 32px;
  height: 32px;
  margin-top: -10px;
  margin-left: 310px;
  display: none;
  position: absolute;
  background: #ff8484;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  -webkit-border-radius: 10px;
  -moz-border-radius: 10px;
  -ms-border-radius: 10px;
  -o-border-radius: 10px;
  cursor: pointer;
  img {
    padding: 8px;
  }
}
.content {
  padding: 16px 16px 24px 16px;
}
</style>
