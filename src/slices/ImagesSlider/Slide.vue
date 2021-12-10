<template>
	<figure class="es-images-slider__slide">
		<PrismicImage
			v-if="image.url"
			:field="image"
			class="es-images-slider__slide__image"
		/>
		<PrismicRichText
			v-if="$prismic.asText(description)"
			:field="description"
			wrapper="figcaption"
			class="es-images-slider__slide__description"
		/>
	</figure>
</template>

<script>
export default {
	props: {
		image: {
			type: Object,
			required: true,
		},
		description: {
			type: Array,
			required: true,
		},
	},
};
</script>
