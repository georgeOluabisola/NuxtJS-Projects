<template>
  <div class="single-post-page">
    <section class="post">
      <h1 class="post-title">{{ loadedPost.title }}</h1>
      <div class="post-details">
          <div class="post-detail">Last update on {{ loadedPost.updatedDate | date }}</div>
          <div class="post-detail">Written by {{ loadedPost.author }}</div>
      </div>
      <p class="post-content">{{ loadedPost.content }}</p>
    </section>
    <section class="post-feedback">
      <p>let me know what you think about the post <a href="mailto:fghfg@gmail.com">fghfg@gmail.com</a></p>
    </section>
  </div>
</template>

<script>

  export default {
    // asyncData(context, callback){
    //   setTimeout(()=>{
    //     callback(null, {
    //       loadedPost: {
    //          id: "1",
    //          title: "First Post (ID: " + context.route.params.id  +  ")",
    //          previewText: "this is our first post",
    //          auhtor: "Bizo",
    //          updatedDate: new Date(),
    //          content: "some dummy text",
    //          thumbnail: "vchchchhchchch"
    //       }
    //     });
    //   }, 1000);
    // }

    asyncData(context)
    {
      if(context.payload)
      {
        return {
          loadedPost: context.payload.postData,
        }
      }
      
      return context.app.$axios.$get('/posts/' + context.params.id + ".json")
      .then(data => {
         return { loadedPost: data };

      })
      .catch(e => context.error(e));
    },
    head: {
      title: 'A blog Post'
    }
  }
</script>

<style scoped>
  .single-post-page {
  padding: 30px;
  text-align: center;
  box-sizing: border-box;
}

.post {
  width: 100%;
}

@media (min-width: 768px) {
  .post {
    width: 600px;
    margin: auto;
  }
}

.post-title {
  margin: 0;
}

.post-details {
  padding: 10px;
  box-sizing: border-box;
  border-bottom: 3px solid #ccc;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

@media (min-width: 768px) {
  .post-details {
    flex-direction: row;
  }
}

.post-detail {
  color: rgb(88, 88, 88);
  margin: 0 10px;
}

.post-feedback a {
  color: red;
  text-decoration: none;
}

.post-feedback a:hover,
.post-feedback a:active {
  color: salmon;
}
</style>
