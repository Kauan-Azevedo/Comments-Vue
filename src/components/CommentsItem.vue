<template>
  <div class="container">
    <h1>Comentarios</h1>
    <hr />
    <div class="form-todo form-group">
      <p>
        <input
          type="text"
          placeholder="nome"
          name="author"
          class="form-control"
          v-model="name"
        />
      </p>
      <p>
        <textarea
          name="message"
          cols="30"
          rows="10"
          placeholder="comentario"
          class="form-control"
          v-model="message"
        ></textarea>
      </p>
      <button class="btn btn-success" type="submit" v-on:click="addComent">
        Comentar
      </button>
    </div>
    <div class="list-group">
      <div
        class="list-group-item"
        v-for="(comment, index) in allComments"
        :key="index"
      >
        <span class="comment__author">
          <strong>
            {{ comment.name }}
          </strong>
        </span>
        <p>{{ comment.message }}</p>
        <div>
          <button class="btn btn-danger" v-on:click="removeComment(index)">
            Exlcluir
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    let itens = JSON.parse(localStorage.getItem('comments'))


    console.log(typeof(itens), itens)
    return {
      comments: itens,
      name: "",
      message: "",
    };
  },
  methods: {
    addComent() {
      if (this.message.trim() === "") {
        return;
      }
      this.comments.push({
        name: this.name,
        message: this.message,
      });

      this.name = "";
      this.message = "";
    },
    removeComment(index) {
      this.comments.splice(index, 1);
    },
  },
  computed: {
    allComments() {
      return this.comments.map((comment) => ({
        ...comment,
        name: comment.name.trim() === "" ? "Anônimo" : comment.name,
      }));
    },
  },
  watch: {
    comments(val) {

      let commentsJSON = JSON.parse(localStorage.getItem('Comments'))

      if(commentsJSON != null){

        localStorage.setItem('comments', JSON.stringify(val))
      } else {
        localStorage.setItem('comments', JSON.stringify(val))
      }

    },
  },
};
</script>
