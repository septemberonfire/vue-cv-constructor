<script>
export default {
  emits: ["load"],
  props: ["comments"],
};
</script>

<template>
  <div class="container">
    <div>
      <button
        class="btn primary"
        @click="$emit('load')"
        v-if="comments.length === 0"
      >
        Загрузить комментарии
      </button>
    </div>
    <div class="card" v-if="comments.length">
      <h2>Комментарии</h2>
      <ul class="list">
        <li class="list-item" v-for="comment in comments" :key="comment.id">
          <div>
            <p>
              <strong>{{ comment.email }}</strong>
            </p>
            <small>{{ comment.name }}</small>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<style></style>
