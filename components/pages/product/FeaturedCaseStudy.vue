<template lang="pug">
#FeaturedCaseStudy
  .case-study-title(v-in-viewport.once) {{ copy.title }}
  .case-study-case
    .case-study-image(v-in-viewport.once,:style="`background-image: url(${copy.image})`")
    .case-study-copy
      .case-study-quote(v-in-viewport.once) {{ copy.quote }}
      .case-study-author(v-in-viewport.once) {{ copy.author }}
  .case-study-cta(v-in-viewport.once)
    CtaButton(
      v-if="buttonCopy !== 'DISABLED'",
      :locale="false",
      :link="`blog/${slug(copy.blog.title)}-${copy.blog.id}`",
      :name="buttonCopy",
      theme="dark-border")
</template>
<script>
import CtaButton from '~/components/buttons/CtaButton'
import inViewportDirective from 'vue-in-viewport-directive'
import { mapGetters } from 'vuex'
const getSlug = require('speakingurl')
export default {
  components: { CtaButton },
  directives: { 'in-viewport': inViewportDirective },
  props: {
    buttonCopy: {
      type: String,
      required: true,
    },
    copy: {
      type: Object,
      required: true,
    },
  },
  data () {
    return {
    }
  },
  computed: { ...mapGetters(['is_en', 'is_not_en', 'is_jp']), },
  methods: {
    slug (title) {
      return getSlug(title)
    },
  },
}
</script>

<style lang="stylus">
@import '../../../assets/stylus/guide/includes/*'
#FeaturedCaseStudy
  background-color not-white
  padding 60px 0

.case-study-title
  text-align center
  color fire-bush
  font-h4()
  padding 0 0 30px 0
  inViewportBottom(0)

.case-study-case
  width 780px
  margin auto

.case-study-image
  float left
  width 140px
  height 140px
  background-color fire-bush
  background-size cover
  background-position 50% 50%
  border-radius 70px
  inViewportBottom(0.1)

.case-study-copy
  padding 20px 0 0 180px

.case-study-quote
  font-h4()
  inViewportBottom(0.2)
.case-study-author
  padding 10px 0 0 0
  font-s2()
  inViewportBottom(0.3)

.case-study-cta
  padding 60px 0 0 0
  text-align center
  inViewportBottom(0.4)

@media all and (min-width: 1px) and (max-width: 1000px)
  #FeaturedCaseStudy
    .case-study-case
      width auto
    .case-study-image
      float none
      margin auto
    .case-study-copy
      padding 20px
      text-align center
    .case-study-quote
      font-s2b()
      line-height 16px
    .case-study-cta
      padding 30px 0 0 0

</style>
