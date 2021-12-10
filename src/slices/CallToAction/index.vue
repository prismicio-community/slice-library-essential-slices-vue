<template>
	<section
		:data-slice-type="slice.slice_type"
		:data-slice-variation="slice.variation"
		class="essential-slice es-bounded es-call-to-action"
	>
		<div class="es-bounded__content es-call-to-action__content">
			<PrismicImage
				v-if="slice.primary.iconImage.url"
				:field="slice.primary.iconImage"
				class="es-call-to-action__image"
			/>
			<div class="es-call-to-action__content">
				<PrismicText
					v-if="$prismic.asText(slice.primary.title)"
					:field="slice.primary.title"
					wrapper="h2"
					class="es-call-to-action__content__heading"
				/>
				<PrismicRichText
					v-if="$prismic.asText(slice.primary.paragraph)"
					:field="slice.primary.paragraph"
					wrapper="div"
					class="es-call-to-action__content__paragraph"
				/>
			</div>
			<ButtonLink
				:field="slice.primary.buttonLink"
				variant="green"
				class="es-call-to-action__button"
			>
				{{ slice.primary.buttonLabel || "Learn more…" }}
			</ButtonLink>
		</div>
	</section>
</template>

<script>
import { getSliceComponentProps } from "@prismicio/vue/components";

import ButtonLink from "../../components/ButtonLink.vue";

export default {
	components: {
		ButtonLink,
	},
	// The array passed to `getSliceComponentProps` is purely optional and acts as a visual hint for you
	props: getSliceComponentProps(["slice", "index", "slices", "context"]),
};
</script>
