<template>
    <main>
      <h1>Swipe them quotes</h1>
        <vue-swing
          @throwout="onThrowout"
          :config="config"
          ref="vueswing"
          class="swing"
        >
          <article v-for="post in random" :key="post.id">
              {{ post.fields.quote }}
            </article>
        </vue-swing>
    </main>
</template>

<script>
import { createClient } from '~/plugins/contentful.js';
import shuffle from 'shuffle-array';
import VueSwing from 'vue-swing';

const client = createClient();

export default {
  components: { VueSwing },
  data: function() {
    return {
      posts: [],
      config: {}
    };
  },
  methods: {
    remove() {
      this.swing();
      setTimeout(() => {
        this.posts.pop();
      }, 100);
    },
    swing() {
      const posts = this.$refs.vueswing.cards;
      posts[posts.length - 1].throwOut(
        Math.random() * 10000 - 50,
        Math.random() * 10000 - 50
      );
    },
    onThrowout ({ target, throwDirection }) {
      const parent = document.getElementsByClassName('swing')[0]
      target.setAttribute('style', 'opacity: 0')

      window.setTimeout(() => {
        parent.removeChild(target)
      }, 200)
    }
  },
  async asyncData({ env }) {
    const posts = await client.getEntries();

    return {
      posts: posts.items
    };
  },
  computed: {
    random: function() {
      return shuffle(this.posts);
    }
  }
};
</script>

<style lang="scss" scoped>
article {
  position: absolute;
  background: #f3f0ec;
  border-radius: 18px;
  width: 390px;
  height: 490px;
  max-height: 80vh;
  max-width: 80vw;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
  font-weight: 300;
  font-size: 38px;
  color: #1f1f11;
  letter-spacing: 0;
  text-align: center;
  line-height: 1.2;
  padding-top: 30px;
  border: 10px solid #fff;
  opacity: 1;
  transition: all 200ms ease;

  @media (max-width: 600px) {
    font-size: 32px;
  }
}
h1 {
  color: #f3f0ec;
  text-align: center;
  margin: 20px 0;
}

.swing {
  position: absolute;
  top: calc(50% + 30px);
  left: 50%;
  width: 400px;
  height: 500px;
  max-height: 80vh;
  max-width: 80vw;
  transform: translateX(-50%) translateY(-50%);
}

</style>
