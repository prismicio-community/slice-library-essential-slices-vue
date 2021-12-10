<template>
	<section
		:data-slice-type="slice.slice_type"
		:data-slice-variation="slice.variation"
		class="essential-slice es-bounded es-pricing-table"
	>
		<div class="es-bounded__content es-pricing-table__content">
			<div class="es-pricing-table__intro">
				<PrismicText
					v-if="$prismic.asText(slice.primary.eyebrowHeadline)"
					:field="slice.primary.eyebrowHeadline"
					wrapper="p"
					class="es-pricing-table__intro__eyebrow"
				/>
				<PrismicText
					v-if="$prismic.asText(slice.primary.title)"
					:field="slice.primary.title"
					wrapper="h2"
					class="es-pricing-table__intro__headline"
				/>
				<PrismicRichText
					v-if="$prismic.asText(slice.primary.description)"
					:field="slice.primary.description"
					wrapper="div"
					class="es-pricing-table__intro__description"
				/>
			</div>
			<ul v-if="slice.items.length > 0" class="es-pricing-table__plans">
				<li
					v-for="(item, index) in slice.items"
					:key="$prismic.asText(item.planTitle)"
					class="es-pricing-table__plan"
				>
					<PlanCard
						:variant="index % 2 ? 'white' : 'beige'"
						:title="item.planTitle"
						:price-option="item.priceOption"
						:features="item.features"
						:call-to-action="item.callToAction"
						:call-to-action-text="item.callToActionText"
						class="es-pricing-table__plan__card"
					/>
				</li>
			</ul>
		</div>
	</section>
</template>

<script>
import { getSliceComponentProps } from "@prismicio/vue/components";

import PlanCard from "./PlanCard.vue";

export default {
	components: {
		PlanCard,
	},
	// The array passed to `getSliceComponentProps` is purely optional and acts as a visual hint for you
	props: getSliceComponentProps(["slice", "index", "slices", "context"]),
};
</script>
