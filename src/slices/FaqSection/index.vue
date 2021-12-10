<template>
	<section
		:data-slice-type="slice.slice_type"
		:data-slice-variation="slice.variation"
		class="essential-slice es-bounded es-faq-section"
	>
		<div class="es-bounded__content es-faq-section__content">
			<div class="es-faq-section__intro">
				<PrismicText
					v-if="$prismic.asText(slice.primary.eyebrowHeadline)"
					:field="slice.primary.eyebrowHeadline"
					wrapper="p"
					class="es-faq-section__intro__eyebrow"
				/>
				<PrismicText
					v-if="$prismic.asText(slice.primary.title)"
					:field="slice.primary.title"
					wrapper="h2"
					class="es-faq-section__intro__headline"
				/>
				<PrismicRichText
					v-if="$prismic.asText(slice.primary.description)"
					:field="slice.primary.description"
					wrapper="div"
					class="es-faq-section__intro__description"
				/>
			</div>
			<div
				class="es-faq-section__primary-content"
				:class="{
					'es-faq-section__primary-content--with-image':
						slice.primary.optionalImage.url,
				}"
			>
				<PrismicImage
					v-if="slice.primary.optionalImage.url"
					:field="slice.primary.optionalImage"
					class="es-faq-section__primary-content__image"
				/>
				<ul
					v-if="slice.items.length > 0"
					class="es-faq-section__primary-content__questions"
				>
					<li
						v-for="item in slice.items"
						:key="$prismic.asText(item.title)"
						class="es-faq-section__question"
					>
						<Question :title="item.title" :text="item.text" />
					</li>
				</ul>
			</div>
		</div>
	</section>
</template>

<script>
import { getSliceComponentProps } from "@prismicio/vue/components";

import Question from "./Question.vue";

export default {
	components: {
		Question,
	},
	// The array passed to `getSliceComponentProps` is purely optional and acts as a visual hint for you
	props: getSliceComponentProps(["slice", "index", "slices", "context"]),
};
</script>
