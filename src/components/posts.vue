<template>
  <div>
    <div>
      <h1>List of posts</h1>
    </div>
    <ul v-for="post in posts" :key="post.id">
      <div v-if="!isEditMode && postId === post.id">
        <div style="border: none;">
          <b>Title:</b>
          <input class="news-input" v-model="post.title" placeholder="post.title">
        </div>
        <div style="border: none;">
          <b>Description:</b>
          <textarea class="news-textarea" v-model="post.description" placeholder="post.description">
          </textarea>
        </div>
        <button @click="update(post)"> Update</button>
      </div>
      <div v-else style="list-style: none">
        <li><b>Title:</b> {{ post.title }}</li>
        <li><b>Description:</b> {{ post.description }}</li>
        <button @click="update(post)"> Edit</button>
        <button @click="archive(post.id)"> Archive</button>
      </div>
    </ul>
    <div>
      <div>
        <h1>Archived posts</h1>
      </div>
      <ul v-for="archivedPost in bin" :key="archivedPost.id" style="list-style: none">
        <li><b>Title:</b> {{ archivedPost.title }}</li>
        <li><b>Description:</b> {{ archivedPost.description }}</li>
        <button @click="recover(archivedPost.id)"> Recover</button>
        <button @click="remove(archivedPost.id)"> Delete</button>
      </ul>
    </div>
  </div>
</template>

<script>
import fixtures from '../data/fixtures';

export default {
  name: 'Posts',
  data() {
    return {
      posts: fixtures,
      postId: '',
      postTitle: '',
      postDescription: '',
      isEditMode: false,
      bin: [],
    };
  },
  methods: {
    // function to send data to bin
    archive(selectedPostId) {
      const index = this.posts.findIndex(post => post.id === selectedPostId);
      const archivePost = this.posts[index];

      this.bin.push(archivePost);
      this.posts.splice(index, 1);
    },

    // function to delete data
    remove(selectedPostId) {
      const index = this.posts.findIndex(post => post.id === selectedPostId);
      this.bin.splice(index, 1);
    },

    // function to recover data
    recover(selectedPostId) {
      // find the post index in the bin
      const index = this.bin.findIndex(post => post.id === selectedPostId);
      const recoverPost = this.bin[index];
      // push into the posts
      this.posts.push(recoverPost);
      // remove posts from bin
      this.bin.splice(index, 1);
    },

    // // function to edit data
    update(selectedPost) {
      // debugger;
      this.isEditMode = !this.isEditMode;

      this.postId = selectedPost.id;
      this.postTitle = selectedPost.title;
      this.postDescription = selectedPost.description;

      const editedPost = {
        title: this.postTitle,
        id: this.postId,
        description: this.postDescription,
      };

      // ..old notebook index
      const index = this.posts.findIndex(post => post.id === selectedPost.id);

      // add the new notebook and remove the old
      this.posts.splice(index, 1, editedPost);
    },
  },
};
</script>

<style>
  .news-input {
    width: 20%;
    margin: 10px 5px;
    padding: 6px 6px;
    box-sizing: border-box;
    border-radius: 10px;
    border: none;
  }

  .news-textarea {
    width: 20%;
    height: 30px;
    padding: 6px 6px;
    box-sizing: border-box;
    border-radius: 10px;
    border: none;
  }
</style>
