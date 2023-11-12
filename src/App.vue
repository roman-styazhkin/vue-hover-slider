<template>
  <div class="container">
    <h1>Hover slider</h1>
    <div class="row">
      <div class="item">
        <vue-hover-slider
					defaultImage="https://madhunter.ru/wp-content/uploads/2019/12/opisanie-lisitsy.jpg"
          :slides="slides"
          :height="350"
					:video="{url: 'https://strm.yandex.ru/vh-canvas-converted/vod-content/3002680902179236855/f12f5132-0a1f-4080-9fd1-6fe67ef7cc37/webm/VP8_854_480_1800.webm?vsid=c9aac6e1679d463447ff4170bd22cefa7e08b496e015xVASx5608x1699780879'}"
        />
				<vue-hover-slider
					defaultImage="https://madhunter.ru/wp-content/uploads/2019/12/opisanie-lisitsy.jpg"
					:slides="slides"
					:height="350"
					:video="{url: 'https://strm.yandex.ru/vh-canvas-converted/vod-content/3002680902179236855/f12f5132-0a1f-4080-9fd1-6fe67ef7cc37/webm/VP8_854_480_1800.webm?vsid=c9aac6e1679d463447ff4170bd22cefa7e08b496e015xVASx5608x1699780879'}"
				/><vue-hover-slider
				defaultImage="https://madhunter.ru/wp-content/uploads/2019/12/opisanie-lisitsy.jpg"
				:slides="slides"
				:height="350"
				:video="{url: 'https://strm.yandex.ru/vh-canvas-converted/vod-content/3002680902179236855/f12f5132-0a1f-4080-9fd1-6fe67ef7cc37/webm/VP8_854_480_1800.webm?vsid=c9aac6e1679d463447ff4170bd22cefa7e08b496e015xVASx5608x1699780879'}"
			/><vue-hover-slider
				defaultImage="https://madhunter.ru/wp-content/uploads/2019/12/opisanie-lisitsy.jpg"
				:slides="slides"
				:height="350"
				:video="{url: 'https://strm.yandex.ru/vh-canvas-converted/vod-content/3002680902179236855/f12f5132-0a1f-4080-9fd1-6fe67ef7cc37/webm/VP8_854_480_1800.webm?vsid=c9aac6e1679d463447ff4170bd22cefa7e08b496e015xVASx5608x1699780879'}"
			/>


        <p>Show all photos</p>
      </div>
    </div>
  </div>
</template>

<script>
import VueHoverSlider from "@/components/VueHoverSlider";

export default {
  name: 'App',
  components: {
    VueHoverSlider
  },
  data: () => ({
    slides: [
			{
				id: 1,
				isVideo: true,
				url: 'https://strm.yandex.ru/vh-canvas-converted/vod-content/3002680902179236855/f12f5132-0a1f-4080-9fd1-6fe67ef7cc37/webm/VP8_854_480_1800.webm?vsid=c9aac6e1679d463447ff4170bd22cefa7e08b496e015xVASx5608x1699780879',
			},

			{
				id: 2,
				url: 'https://s1.1zoom.ru/big3/270/348443-sepik.jpg'
			},

			{
				id: 3,
				url: 'https://madhunter.ru/wp-content/uploads/2019/12/opisanie-lisitsy.jpg',
			}
    ]
  }),
}
</script>

<style lang="scss">
  body {
    font-family: sans-serif;
  }

  .container {
    max-width: 1200px;
    margin: 0 auto;
  }

  .row {
    display: flex;
    flex-wrap: wrap;
    margin-left: -.9375rem;
    margin-right: -.9375rem;
  }

  .item {
    margin-left: .9375rem;
    margin-right: .9375rem;
    width: calc(50% - 1.875rem);
    margin-bottom: 2rem;

    @media (max-width: 767px) {
      width: 100%;
    }
  }
</style>
