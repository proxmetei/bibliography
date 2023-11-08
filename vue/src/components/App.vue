<template>
  <div>
    <div class="main-block">
      <input :value="inputFile" @change="(e) => setFile(e)" type="file" id="import" accept=".json" style="display: none;">
      <div class="main-block-buttons">
        <el-button type="primary" @click="() => openFile()">
          Импорт
        </el-button>
        <a :href = "downloadRef" class="el-button el-button--primary" download="file.json" type="primary">
         <span>Экспорт</span>
        </a>
      </div>
      <div class="main-block-content">
        <ListContainer :books="books" :type-list="typeOfList" />
        <div>
          <el-select v-model="typeOfList" placeholder="Выберите тип списка">
            <el-option
              v-for="item in options" 
              :key="item.value" 
              :label="item.label" 
              :value="item.value"
            >
            </el-option>
          </el-select>
        </div>
      </div>
    </div>
    <RouterView />
    <ModalContainer />
    <BookForm />
  </div>
</template>

<script>
import ModalContainer from "@/components/parts/ModalContainer";
import ListContainer from "@/components/List.vue";
import BookForm from "@/components/BookForm.vue";
import {mapGetters, mapMutations} from "vuex";

export default {
  components: {
    ModalContainer,
    BookForm,
    ListContainer
  },
  data () {
    return {
      typeOfList: 'div',
      inputFile: null,
      options: [{
        value: "ul",
        label: "Простой список"
      }, {
        value: "ol",
        label: "Нумерованный список"
      }, {
        value: "div",
        label: "По умолчанию"
      }]
    }
  },
  computed: {
    ...mapGetters('books', [
      'getBooks'
    ]),
    books () {
      return this.getBooks
    },
    downloadRef () {
      return "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(this.books));
    } 
  },
  methods: {
    ...mapMutations('books', [
      'setBooks'
    ]),
    setFile (e) {
      let reader = new FileReader();
      reader.onload = (e) => {
        this.setBooks(JSON.parse(e.target.result));
      }
      reader.readAsText(e.target.files[0]);
    },
    openFile () {
      document.getElementById("import").click();
    }
  }
}
</script>

<style lang="less">
@import url('https://fonts.googleapis.com/css2?family=Jost:wght@400;700&display=swap');

.main-block {
  display: flex;
  justify-content: center;

  &-content {
    background-color: @cBaseOne;
  }
}

.main-block-buttons .el-button--primary {
  font-size: 20px !important;
  font-family: 'Times New Roman', Times, serif;
  font-style: normal  !important;
  font-weight: 500 !important;
}

body {
  margin: 0;
  padding: 0;
  background-color: @cBaseTwo;
}

a {
  text-decoration: none;
}

section {
  background-color: @cBaseOne;
  margin-bottom: 20px;
  border-radius: 2px;
  box-sizing: border-box;

  &:last-child {
    margin-bottom: 0;
  }
}

h1, h2, h3, h4, h5 {
  font-family: @ffOne;
  color: @cBaseThree;
  margin: 0;
}

h2 {
  font-size: 32px;
}

.p-16 {
  padding: 16px;
}

.d-flex {
  display: flex;
}

.rcms {

  &-divider {

    &-h {
      width: 100%;
      height: @sizeBorderDefault;
      background-color: @cBaseTwo;
    }

    &-v {

    }
  }

  &-loading {
    position: relative;

    &::after {
      content: '';
      position: absolute;
      left: 0;
      top: 0;
      right: 0;
      bottom: 0;
      z-index: 1;
      background: rgba(100, 100, 100, 0.5);
      cursor: wait;
    }
  }
}
</style>
