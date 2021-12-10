<template>
	<section
		:data-slice-type="slice.slice_type"
		:data-slice-variation="slice.variation"
		class="essential-slice es-bounded es-cards-carousel"
	>
		<div class="es-bounded__content es-cards-carousel__content">
			<div class="es-cards-carousel__intro">
				<PrismicText
					v-if="$prismic.asText(slice.primary.eyebrowHeadline)"
					:field="slice.primary.eyebrowHeadline"
					wrapper="p"
					class="es-cards-carousel__intro__eyebrow"
				/>
				<PrismicText
					v-if="$prismic.asText(slice.primary.title)"
					:field="slice.primary.title"
					wrapper="h2"
					class="es-cards-carousel__intro__headline"
				/>
				<PrismicRichText
					v-if="$prismic.asText(slice.primary.description)"
					:field="slice.primary.description"
					wrapper="div"
					class="es-cards-carousel__intro__description"
				/>
			</div>
			<div v-if="slice.items.length" class="es-cards-carousel__carousel">
				<div
					ref="slider"
					class="es-cards-carousel__carousel__cards keen-slider"
				>
					<div
						v-for="(item, index) in items"
						:key="`${$prismic.asText(item.title)}-${index}`"
						class="es-cards-carousel__card keen-slider__slide"
					>
						<PrismicImage
							v-if="item.image.url.url"
							:field="item.image.url"
							class="es-cards-carousel__card__image"
						/>
						<PrismicText
							v-if="$prismic.asText(item.title)"
							:field="item.title"
							wrapper="h3"
							class="es-cards-carousel__card__title"
						/>
						<PrismicRichText
							v-if="$prismic.asText(item.content)"
							:field="item.content"
							wrapper="div"
							class="es-cards-carousel__card__content"
						/>
					</div>
				</div>
				<button
					aria-label="Previous card"
					class="es-cards-carousel__carousel__control es-cards-carousel__carousel__control--prev"
					@click="prev"
				>
					<ChevronIcon
						direction="left"
						:aria-hidden="true"
						class="es-cards-carousel__carousel__control__icon"
					/>
				</button>
				<button
					aria-label="Next card"
					class="es-cards-carousel__carousel__control es-cards-carousel__carousel__control--next"
					@click="next"
				>
					<ChevronIcon
						direction="right"
						:aria-hidden="true"
						class="es-cards-carousel__carousel__control__icon"
					/>
				</button>
			</div>
		</div>
	</section>
</template>

<script>
import KeenSlider from "keen-slider";

import { getSliceComponentProps } from "@prismicio/vue/components";

import ChevronIcon from "../../components/ChevronIcon.vue";

export default {
	components: {
		ChevronIcon,
	},
	// The array passed to `getSliceComponentProps` is purely optional and acts as a visual hint for you
	props: getSliceComponentProps(["slice", "index", "slices", "context"]),
	computed: {
		items() {
			// The list of cards is duplicated to avoid carousel rendering issues.
			// When less than 4 cards are available, cards will flash into
			// existance on next/prev movements.
			return [...this.slice.items, ...this.slice.items];
		},
	},
	mounted() {
		this.$options.slider = new KeenSlider(this.$refs.slider, {
			loop: true,
			slides: {
				perView: 1,
				spacing: 32,
			},
			breakpoints: {
				"(min-width: 640px)": {
					slides: {
						perView: 2,
						spacing: 32,
					},
				},
				"(min-width: 896px)": {
					slides: {
						perView: 3,
						spacing: 32,
					},
				},
				"(min-width: 1600px)": {
					slides: {
						perView: 4,
						spacing: 32,
					},
				},
			},
		});
	},
	destroyed() {
		this.$options.slider.destroy();
	},
	methods: {
		prev() {
			this.$options.slider.prev();
		},
		next() {
			this.$options.slider.next();
		},
	},
};
</script>
