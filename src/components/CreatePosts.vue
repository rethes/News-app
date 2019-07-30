<template>
  <div>
    <div>
      <h1>Create a news post</h1>
    </div>
    <div>
      <div style="border: none;">
        <b>Title:</b>
        <input class="news-input" placeholder="Add a Title"
               v-model="newTitle">
      </div>
      <div style="border: none;">
        <b>Description:</b>
        <textarea class="news-textarea" placeholder="Add a description"
                  v-model="newDescription">
      </textarea>
      </div>
      <button @click="addPost">Add</button>
      <!--<h2>Description:</h2>-->
      <!--<input placeholder="Add a Description">-->
    </div>
  </div>
</template>

<script>
import cuid from 'cuid';
import fixtures from '../data/fixtures';

export default {
  name: 'CreatePosts',
  // app initial state
  data() {
    return {
      posts2: fixtures,
      newTitle: '',
      newDescription: '',
    };
  },

  // methods that implement data logic.
  // note there's no DOM manipulation here at all.
  methods: {
    addPost() {
      const trimmedTitle = this.newTitle && this.newTitle.trim();
      const trimmedDescription = this.newDescription && this.newDescription.trim();
      if (!trimmedTitle && !trimmedDescription) {
        return;
      }
      const newPost = {
        title: trimmedTitle,
        id: cuid(),
        description: trimmedDescription,
      };

      this.posts2.push(newPost);
      this.newTitle = '';
      this.newDescription = '';
    },
  },
};

</script>
