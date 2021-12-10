<template>
	<figure class="es-testimonials-slider__slide">
		<PrismicImage
			v-if="image.url"
			:field="image"
			class="es-testimonials-slider__slide__image"
		/>
		<figcaption class="es-testimonials-slider__slide__testimonial">
			<PrismicRichText
				v-if="$prismic.asText(description)"
				:field="description"
				wrapper="div"
				class="es-testimonials-slider__slide__testimonial__content"
			/>
			<div class="es-testimonials-slider__slide__testimonial__person">
				<span
					v-if="person"
					class="es-testimonials-slider__slide__testimonial__person__name"
				>
					{{ person }}
				</span>

				<span
					v-if="title"
					class="es-testimonials-slider__slide__testimonial__person__title"
				>
					{{ title }}
				</span>
			</div>
		</figcaption>
	</figure>
</template>

<script>
export default {
	props: {
		image: {
			type: Object,
			required: true,
		},
		testimonial: {
			type: Array,
			required: true,
		},
		person: {
			type: String,
			required: true,
		},
		title: {
			type: String,
			required: true,
		},
	},
};
</script>
