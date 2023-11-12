<template>
<div :style="containerStyles">
  <div class="vue-hover-slider" v-if="slides.length > 0">
    <a v-if="link" :href="link" :target="linkTarget">
      <slides-controls
        :slides="slicedSlides"
        v-model="activeSlide"
      />
    </a>
    <slides-controls
      v-else
      :slides="slicedSlides"
      v-model="activeSlide"
    />
    <div class="vue-hover-slider__images">
			<template v-for="(item, index) in slicedSlides">
				<div
					v-if="!item.isVideo"
					:key="index"
					class="vue-hover-slider__image"
					:class="{'vue-hover-slider__image--visible': activeSlide === index, 'last-slide': index === countSlides-1 && countSlides >= maxSlidesToShow}"
					:style="`background-image: url('${item.url}')`">
        <span v-if="countSlidesLeft" class="vue-hover-slider__image-overlay">
          <span>
            <slot name="more" :count="countSlidesLeft">
              +{{ countSlidesLeft }} {{ countSlidesLeft > 1 ? 'images' : 'image' }}
            </slot>
          </span>
        </span>
				</div>

				<video
					loop="true"
					data-name="video-slot" muted="muted" webkit-playsinline="true" playsinline="" pip="false"
					ref="video"
					:src="item.url"
					class="vue-hover-slider__image"
					autoplay
					:class="{'vue-hover-slider__image--visible': activeSlide === index, 'last-slide': index === countSlides-1 && countSlides >= maxSlidesToShow}" :key="index" v-if="item.isVideo" />
			</template>

    </div>
  </div>
  <a
    v-else-if="link"
    :href="link"
    :target="linkTarget"
    class="vue-hover-slider__image vue-hover-slider__image--visible"
    :style="`background-image: url(${defaultImage})`"></a>
  <div
    v-else
    class="vue-hover-slider__image vue-hover-slider__image--visible"
    :style="`background-image: url(${defaultImage})`"></div>
</div>
</template>

<script>
import SlidesControls from '@/components/VueHoverSlidesControls'

export default {
  name: 'VueHoverSlider',
  components: {
    SlidesControls
  },
  props: {
    slides: {
      type: Array,
      required: true
    },
    link: {
      type: String,
      required: false,
      default: ''
    },
    openInNewTab: {
      type: Boolean,
      required: false,
      default: false
    },
    maxSlidesToShow: {
      type: Number,
      required: false,
      default: Infinity
    },
    defaultImage: {
      type: String,
      required: false,
      default: 'https://savayer.space/img/default_image.jpg'
    },
    height: {
      type: Number,
      required: false,
      default: 250
    }
  },
  data: () => ({
    activeSlide: 0,
    requiredDefaultImage: null
  }),
  computed: {
    linkTarget () {
      return this.openInNewTab ? '_blank' : '_self'
    },
    containerStyles () {
      return {
        height: this.height ? `${this.height}px` : ''
      }
    },
    slicedSlides () {
      return this.slides.slice(0, this.maxSlidesToShow)
    },
    countSlides () {
      return this.slicedSlides.length
    },
    countSlidesLeft () {
      return this.slides.length > this.countSlides ? this.slides.length - this.countSlides : 0
    }
  },
  methods: {
    preloadImages () {
      if (Array.isArray(this.slides) && this.slides.length > 0) {
        this.slides.forEach(slide => {
          const image = new Image()
          image.src = slide
        })
      }
    }
  },
  mounted () {
    this.preloadImages()
		// this.$refs.video[0].play()
  }
}
</script>

<style lang="scss">
.vue-hover-slider {
	position: relative;
	height: 100%;

	&:hover {
		.vue-hover-slider__controls {
			visibility: visible;
		}
	}
}

.vue-hover-slider__images {
	height: 100%;
}

.vue-hover-slider__image {
	border-radius: 5px;
	background-size: cover;
	background-position: center;
	background-repeat: no-repeat;
	display: none;
	outline: none;
	height: 100%;
	width: 100%;

	&--visible {
		display: block;
	}

	&.last-slide {
		position: relative;
	}

	&--visible.last-slide .vue-hover-slider__image-overlay {
		display: flex;
	}
}

.vue-hover-slider__image-overlay {
	position: absolute;
	z-index: 1;
	top: 0;
	left: 0;
	right: 0;
	bottom: 0;
	width: 100%;
	height: 100%;
	background: rgba(68, 68, 68, 0.8);
	display: none;

	span {
		margin: auto;
		color: #fff;
	}
}

.vue-hover-slider__controls {
	position: absolute;
	z-index: 2;
	top: 0;
	left: 0;
	right: 0;
	bottom: 0;
	width: 100%;
	height: 100%;
	display: flex;
	justify-content: space-between;
	visibility: hidden;

	&.hide-controls .vue-hover-slider__control {
		display: none;
	}

	@media (max-width: 767px) {
		visibility: visible;
	}
}

.vue-hover-slider__control {
	flex: 1 1;
	height: calc(100% - 5px);
	position: relative;

	&--active .vue-hover-slider__control-mark{
		background: #277BD0;
	}
}

.vue-hover-slider__control-mark {
	position: absolute;
	bottom: 0;
	left: 3px;
	width: calc(100% - 10px);
	height: 3px;
	background: rgba(214, 214, 214, 0.28);

	@media (max-width: 767px) {
		height: 2px;
	}
}

</style>
