<template>
	<section
		:data-slice-type="slice.slice_type"
		:data-slice-variation="slice.variation"
		class="essential-slice bounded customer-logos"
	>
		<div class="bounded__content customer-logos__content">
			<PrismicText
				v-if="$prismic.asText(slice.primary.eyebrowHeadline)"
				:field="slice.primary.eyebrowHeadline"
				wrapper="h2"
				class="customer-logos__heading"
			/>
			<ul v-if="slice.items.length > 0" class="customer-logos__logos">
				<li
					v-for="item in items"
					:key="item.logo.url"
					class="customer-logos__logo"
				>
					<PrismicLink :field="item.link" class="customer-logos__link">
						<PrismicImage
							:field="item.logo"
							class="customer-logos__logo__link__image"
						/>
					</PrismicLink>
				</li>
			</ul>
			<ButtonLink
				:field="slice.primary.callToActionLink"
				class="customer-logos__button"
			>
				{{ $prismic.asText(slice.primary.callToAction) || "Learn more" }}
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
	computed: {
		items() {
			return this.slice.items.filter((item) => item.logo.url);
		},
	},
};
</script>
