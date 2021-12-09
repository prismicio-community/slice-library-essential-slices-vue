<template>
	<section
		:data-slice-type="slice.slice_type"
		:data-slice-variation="slice.variation"
		class="essential-slice bounded alternate-grid"
	>
		<div
			class="bounded__content alternate-grid__content"
			:class="{
				'alternate-grid__content--with-image': slice.primary.optionalImage.url,
			}"
		>
			<PrismicImage
				v-if="slice.primary.optionalImage.url"
				:field="slice.primary.optionalImage"
				class="alternate-grid__image"
				:class="{
					'alternate-grid__image--left': slice.primary.imageSide === 'left',
					'alternate-grid__image--right': slice.primary.imageSize === 'right',
				}"
			/>
			<div class="alternate-grid__primary-content">
				<div class="alternate-grid__primary-content__intro">
					<PrismicText
						v-if="$prismic.asText(slice.primary.eyebrowHeadline)"
						:field="slice.primary.eyebrowHeadline"
						wrapper="p"
						class="alternate-grid__primary-content__intro__eyebrow"
					/>
					<PrismicText
						v-if="$prismic.asText(slice.primary.title)"
						:field="slice.primary.title"
						wrapper="h2"
						class="alternate-grid__primary-content__intro__headline"
					/>
					<PrismicRichText
						v-if="$prismic.asText(slice.primary.description)"
						:field="slice.primary.description"
						wrapper="div"
						class="alternate-grid__primary-content__intro__description"
					/>
				</div>
				<div
					v-if="slice.items.length > 0"
					class="alternate-grid__primary-content__items"
				>
					<div
						v-for="(item, index) in slice.items"
						:key="`${$prismic.asText(item.title)}-${index}`"
						class="alternate-grid__item"
					>
						<PrismicImage
							v-if="item.optionalIcon.url"
							:field="item.optionalIcon"
							class="alternate-grid__item__icon"
						/>
						<PrismicText
							v-if="$prismic.asText(item.title)"
							:field="item.title"
							wrapper="h3"
							class="alternate-grid__item__heading"
						/>
						<PrismicRichText
							v-if="$prismic.asText(item.description)"
							:field="item.description"
							wrapper="div"
							class="alternate-grid__item__description"
						/>
					</div>
				</div>
			</div>
		</div>
	</section>
</template>

<script>
import { getSliceComponentProps } from "@prismicio/vue/components";

export default {
	// The array passed to `getSliceComponentProps` is purely optional and acts as a visual hint for you
	props: getSliceComponentProps(["slice", "index", "slices", "context"]),
};
</script>
