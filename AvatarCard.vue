<template>
  <div class="uk-grid-collapse" uk-grid>
    <div
        v-if="showModal"
        class="uk-card-default uk-width-1-4 uk-background-muted uk-padding">
      <div class="uk-margin">
        <input
            class="uk-input"
            type="text"
            v-model="imageSrc"
            placeholder="Image-src"
            @input="updateSrc"
        >
      </div>
      <div class="uk-margin">
        <input
            class="uk-range"
            type="range"
            v-model="zoomValue"
            min="1"
            max="5"
            step=".25"
            uk-tooltip="Image zoom"
            @input="updateZoom"
        >
      </div>
      <div class="uk-margin">
        <input
            class="uk-range"
            type="range"
            v-model="offsetVertical"
            :min="offsetVerticalMin"
            :max="offsetVerticalMax"
            step="0.5"
            uk-tooltip="Vertical position"
            @input="updateOffsetVertical"
        >
      </div>
      <div class="uk-margin">
        <input
            class="uk-range"
            type="range"
            v-model="offsetHorizontal"
            :min="offsetHorizontalMin"
            :max="offsetHorizontalMax"
            step="0.5"
            uk-tooltip="Horizontal position"
            @input="updateOffsetHorizontal"
        >
      </div>
    </div>
    <div
        class="uk-card uk-card-default uk-width-1-2@m"
        @click="toggleModal"
    >
      <div class="uk-card-header">
        <div class="uk-grid-small uk-flex-middle" uk-grid>
          <div class="uk-width-auto">
            <div class="circular-frame">
              <img
                  width="60"
                  height="60"
                  :src="imageSrc"
                  :style="imageStyle"
                  @click.stop="toggleModal">
            </div>
          </div>
          <div class="uk-width-expand">
            <h3
                class="uk-card-title uk-margin-remove-bottom uk-align-right"
                @click.stop=""
            >Title</h3>
            <p
                class="uk-text-small uk-margin-remove-top uk-align-right"
                @click.stop=""
            >Subtitle</p>
          </div>
        </div>
      </div>
      <div class="uk-card-body">
        <p @click.stop="">
          Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolores doloribus eius, fugit modi
          quidem totam!
          Consectetur odio quae rem? Ab aliquam assumenda at consequatur, debitis dolores enim eveniet fuga fugiat
          molestias natus neque, obcaecati odit porro provident quam rerum similique sit, sunt voluptate? Alias culpa
          dolorum, ea et libero numquam possimus! Error fugit iure nam rem repellat. Ad, quod vero?
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import {computed, ref} from "vue";

export default {
  name: "AvatarCard",
  setup() {
    const showModal = ref(false)
    const toggleModal = () => showModal.value = !showModal.value
    // src
    const imageSrc = ref('https://images.unsplash.com/photo-1563823856120-88d1fe6b75bc?ixlib=rb-1.2.1&q=99&fm=jpg&crop=entropy&cs=tinysrgb&w=2048&fit=max&ixid=eyJhcHBfaWQiOjcwOTV9')
    const updateSrc = event => imageSrc.value = event.target.value
    // zoom
    const zoomValue = ref(1)
    const updateZoom = event => zoomValue.value = event.target.value
    // offset vertical
    const offsetVertical = ref(0)
    const offsetVerticalMin = computed(() => (zoomValue.value - 1) * -10)
    const offsetVerticalMax = computed(() => (zoomValue.value - 1) * 10)
    const updateOffsetVertical = event => offsetVertical.value = event.target.value
    // offset horizontal
    const offsetHorizontal = ref(0)
    const offsetHorizontalMin = computed(() => (zoomValue.value - 1) * -10)
    const offsetHorizontalMax = computed(() => (zoomValue.value - 1) * 10)
    const updateOffsetHorizontal = event => offsetHorizontal.value = event.target.value

    const imageStyle = computed(() => {
      return {
        transform: `scale(${ zoomValue.value }) translate(${ offsetVertical.value }%, ${ offsetHorizontal.value }%)`,
      }
    })

    return {
      imageSrc,
      imageStyle,
      offsetHorizontal,
      offsetHorizontalMin,
      offsetHorizontalMax,
      offsetVertical,
      offsetVerticalMin,
      offsetVerticalMax,
      showModal,
      toggleModal,
      updateOffsetHorizontal,
      updateOffsetVertical,
      updateSrc,
      updateZoom,
      zoomValue,
    }
  }
}
</script>

<style scoped>
.circular-frame {
  display: inline-block;
  position: relative;
  width: 100px;
  height: 100px;
  overflow: hidden;
  border-radius: 50%;
}

.circular-frame img {
  width: auto;
  height: 100%;
}
</style>
