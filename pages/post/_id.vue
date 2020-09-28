<template>
    <article class="post">
      <header class="post-header">
        <div class="post-title">
          <h1>Post title</h1>
          <nuxt-link to="/">
            <i class="el-icon-back"></i>
          </nuxt-link>
        </div>
        <div class="post-info">
          <small>
            <i class="el-icon-time"></i>
            {{ new Date().toLocaleString() }}
          </small>
          <small>
            <i class="el-icon-view"></i>
            42
          </small>
        </div>
        <div class="post-img">
          <img src="https://www.amigo-s.ru/content-images/b5fe743bbdc6f27dbdaf0dbae32ae4b9.jpg"
               alt="post image">
        </div>
      </header>
      <main class="post-content">
          <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit.
          Dicta dignissimos earum eius harum illo in repudiandae tenetur.
          Alias aliquam assumenda deserunt dignissimos eaque enim itaque, magnam, nisi quis tempore vel!</p>
          <p>Ad, animi dolore eaque ipsum minima omnis quaerat quasi quisquam quod vero! At consequatur deserunt earum illum nobis numquam,
            omnis quod rem sapiente sed, tempora voluptates! Adipisci at enim quo.</p>
          <p>At deleniti enim error inventore ipsum itaque laudantium minus natus, necessitatibus officiis perferendis quas repellendus sed sint
            ut vel voluptatum? Consectetur deleniti dolorum ex minus mollitia numquam sequi, tempore vero.</p>
          <p>Amet aperiam assumenda atque consectetur corporis dolor, doloribus dolorum eaque enim fuga ipsa itaque laudantium libero
            mollitia nihil nisi numquam odio, officiis quaerat, quibusdam quis quos sed similique suscipit voluptate?</p>
          <p>Architecto deserunt excepturi ipsum neque porro voluptas. Cumque ex facere libero neque nulla placeat quia quidem unde.
            Accusantium alias autem cum, dignissimos, ea expedita facilis fugit hic inventore minus temporibus!</p>
          <p>Alias aspernatur commodi doloribus nobis placeat, quae quos rem tempore tenetur ut. Ab consequatur consequuntur deleniti illum incidunt
            itaque laborum necessitatibus neque officiis perferendis, quisquam recusandae tenetur ut vero voluptatibus.</p>
          <p>Amet animi aperiam architecto aut autem beatae cum deleniti dignissimos dolor doloribus, dolorum ducimus et eum expedita impedit in ipsam iure
            libero minima necessitatibus officiis quo rem, sint, ut voluptatibus!</p>
          <p>Amet doloribus ea eaque illo illum inventore iste laudantium minima
            nisi obcaecati praesentium quia ratione, tenetur totam ut voluptatem voluptatibus! Aliquam doloremque error esse natus nihil nisi quasi quisquam velit.</p>
          <p>Ab adipisci est et hic, id impedit minus quidem quisquam. Accusantium aliquid deleniti eaque eius enim error eveniet laboriosam odit officia officiis,
            porro quae quia rerum unde vitae. A, porro!</p>
      </main>
      <footer>
        <app-comment-form
              v-if="canAddComment"
              @created="createCommentHandler"/>
        <div class="comments" v-if="true">
          <app-comment
          v-for="comment in 4"
          :key="comment"
          :comment="comment"/>
        </div>
        <div class="text-center" v-else>Комментариев нет</div>
      </footer>
    </article>
</template>

<script>
  import AppComment from '@/components/main/Comment'
  import AppCommentForm from '@/components/main/CommentForm'
    export default {
      validate({params}) {
        return !!params.id
      },
      data() {
        return {
          canAddComment: true
        }
      },
      methods: {
        createCommentHandler() {
          this.canAddComment = false
        }
      },
      components: {
        AppComment,
        AppCommentForm
      }
    }
</script>

<style lang="scss" scoped>
  .post {
    max-width: 1100px;
    margin: 0 auto;
  }
  .post-title {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 1rem;
  }

  .post-info {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: .5rem;
  }

  .post-img {
    margin: 1.5rem 0 2rem;

    img {
      width: 100%;
      height: auto;
    }
  }
  .post-content {
    margin-bottom: 2rem;
  }
</style>
