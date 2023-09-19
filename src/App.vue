<template>
  <div>
    <div class="container column">
      <form class="card card-w30">
        <div class="form-control">
          <label for="type">Тип блока</label>
          <select id="type" v-model="selector">
            <option value="title">Заголовок</option>
            <option value="subtitle">Подзаголовок</option>
            <option value="avatar">Аватар</option>
            <option value="text">Текст</option>
          </select>
        </div>

        <div class="form-control">
          <label for="value">Значение</label>
          <textarea id="value" rows="3" v-model="input"></textarea>
        </div>

        <button
          class="btn primary"
          @click.prevent="buttonHandler"
          :disabled="input.length < 3"
        >
          Добавить
        </button>
      </form>

      <div class="card card-w70">
        <Block type="title">{{ title }}</Block>
        <Avatar :avatarUrl="avatarUrl"></Avatar>
        <h3 v-if="blocks.length === 0">
          Добавьте первый блок, чтобы увидеть результат
        </h3>
        <template v-for="(item, idx) in blocks" :key="idx">
          <Block :type="item.type">{{ item.content }}</Block>
        </template>
      </div>
    </div>
    <div class="loader" v-if="loading === true"></div>
    <Comments :comments="comments" @load="loadComments"> </Comments>
  </div>
</template>

<script>
import Avatar from "./components/Avatar.vue";
import Block from "./components/Block.vue";
import Comments from "./components/Comments.vue";
import axios from "axios";
export default {
  data() {
    return {
      loading: false,
      comments: [],
      input: "",
      selector: "title",
      title: "CV Rick",
      avatarUrl:
        "https://cdn.dribbble.com/users/5592443/screenshots/14279501/drbl_pop_r_m_rick_4x.png",
      blocks: [
        {
          type: "subtitle",
          content: "Опыт работы",
        },
        {
          type: "text",
          content: `главный герой американского мультсериала «Рик и Морти», гениальный
          учёный, изобретатель, атеист (хотя в некоторых сериях он даже молится
          Богу, однако, каждый раз после чудесного спасения ссылается на удачу и
          вновь отвергает его существование), алкоголик, социопат, дедушка
          Морти. На момент начала третьего сезона ему 70 лет[1]. Рик боится
          пиратов, а его главной слабостью является некий - "Санчезиум". Исходя
          из того, что существует неограниченное количество вселенных,
          существует неограниченное количество Риков, герой сериала
          предположительно принадлежит к измерению С-137. В серии комикcов Рик
          относится к измерению C-132, а в игре «Pocket Mortys» — к измерению
          C-123[2]. Прототипом Рика Санчеза является Эмметт Браун, герой
          кинотрилогии «Назад в будущее»[3].`,
        },
      ],
    };
  },
  methods: {
    changeTitle() {
      this.title = this.input;
    },
    changeAvatar() {
      this.avatarUrl = this.input;
    },
    addBlock(type) {
      this.blocks.push({
        type: type,
        content: this.input,
      });
    },
    buttonHandler() {
      switch (this.selector) {
        case "title":
          this.changeTitle();
          break;
        case "avatar":
          this.changeAvatar();
          break;
        case "subtitle":
          this.addBlock("subtitle");
          break;
        case "text":
          this.addBlock("text");
          break;
        default:
          console.log(this.selector);
          break;
      }
      this.input = "";
    },
    async loadComments() {
      this.loading = true;
      const res = await axios.get(
        "https://jsonplaceholder.typicode.com/comments?_limit=42"
      );
      this.comments = res.data;
      this.loading = false;
    },
  },
  components: { Avatar, Block, Comments },
};
</script>

<style>
.avatar {
  display: flex;
  justify-content: center;
}

.avatar img {
  width: 150px;
  height: auto;
  border-radius: 50%;
}
</style>
