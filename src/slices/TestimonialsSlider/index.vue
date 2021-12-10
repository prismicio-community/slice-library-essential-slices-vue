<template>
	<section
		:data-slice-type="slice.slice_type"
		:data-slice-variation="slice.variation"
		class="essential-slice es-bounded es-testimonials-slider"
	>
		<div class="es-bounded__content es-testimonials-slider__content">
			<div class="es-testimonials-slider__intro">
				<PrismicText
					v-if="$prismic.asText(slice.primary.eyebrowHeadline)"
					:field="slice.primary.eyebrowHeadline"
					wrapper="p"
					class="es-testimonials-slider__intro__eyebrow"
				/>
				<PrismicText
					v-if="$prismic.asText(slice.primary.title)"
					:field="slice.primary.title"
					wrapper="h2"
					class="es-testimonials-slider__intro__headline"
				/>
				<PrismicRichText
					v-if="$prismic.asText(slice.primary.paragraph)"
					:field="slice.primary.paragraph"
					wrapper="div"
					class="es-testimonials-slider__intro__description"
				/>
			</div>
			<div v-if="slice.items.length > 0" class="es-testimonials-slider__slider">
				<ul
					ref="slider"
					class="es-testimonials-slider__slider__slides keen-slider"
				>
					<li
						v-for="item in items"
						:key="item.image.url"
						class="es-testimonials-slider__slider__slide keen-slider__slide"
					>
						<Slide
							:image="item.image"
							:testimonial="item.testimonial"
							:person="item.person"
							:title="item.title"
						/>
					</li>
				</ul>
				<div class="es-testimonials-slider__slider__controls">
					<button
						v-for="(item, index) in items"
						:key="item.image.url"
						:aria-label="`Go to slide ${index + 1}`"
						class="es-testimonials-slider__slider__dot-control"
						@click="moveToIdx(index)"
					>
						<div
							class="es-testimonials-slider__slider__dot-control__dot"
							:class="{
								'es-testimonials-slider__slider__dot-control__dot--active':
									activeSlideIndex === index,
							}"
						/>
					</button>
					<button
						aria-label="Previous card"
						class="es-testimonials-slider__slider__arrow-control es-testimonials-slider__slider__arrow-control--prev"
						@click="prev"
					>
						<ChevronIcon
							direction="left"
							:aria-hidden="true"
							class="es-testimonials-slider__slider__arrow-control__icon"
						/>
					</button>
					<button
						aria-label="Next card"
						class="es-testimonials-slider__slider__arrow-control es-testimonials-slider__slider__arrow-control--next"
						@click="next"
					>
						<ChevronIcon
							direction="right"
							:aria-hidden="true"
							class="es-testimonials-slider__slider__arrow-control__icon"
						/>
					</button>
				</div>
			</div>
		</div>
	</section>
</template>

<script>
import KeenSlider from "keen-slider";

import { getSliceComponentProps } from "@prismicio/vue/components";

import ChevronIcon from "../../components/ChevronIcon.vue";
import Slide from "./Slide.vue";

export default {
	components: {
		ChevronIcon,
		Slide,
	},
	// The array passed to `getSliceComponentProps` is purely optional and acts as a visual hint for you
	props: getSliceComponentProps(["slice", "index", "slices", "context"]),
	data() {
		return {
			activeSlideIndex: 0,
		};
	},
	computed: {
		items() {
			return this.slice.items.filter((item) => item.image.url);
		},
	},
	mounted() {
		this.$options.slider = new KeenSlider(this.$refs.slider, {
			loop: true,
			slides: { perView: 1 },
			slideChanged: (slider) => {
				this.activeSlideIndex = slider.track.details.rel;
			},
		});
	},
	destroyed() {
		this.$options.slider.destroy();
	},
	methods: {
		moveToIdx(index) {
			this.$options.slider.moveToIdx(index);
		},
		prev() {
			this.$options.slider.prev();
		},
		next() {
			this.$options.slider.next();
		},
	},
};
</script>
