<template>
	<section
		:data-slice-type="slice.slice_type"
		:data-slice-variation="slice.variation"
		class="essential-slice es-bounded es-video-highlights"
	>
		<div class="es-bounded__content es-video-highlights__content">
			<div class="es-video-highlights__intro">
				<PrismicText
					v-if="$prismic.asText(slice.primary.eyebrowHeadline)"
					:field="slice.primary.eyebrowHeadline"
					wrapper="p"
					class="es-video-highlights__intro__eyebrow"
				/>
				<PrismicText
					v-if="$prismic.asText(slice.primary.title)"
					:field="slice.primary.title"
					wrapper="h2"
					class="es-video-highlights__intro__headline"
				/>
				<PrismicRichText
					v-if="$prismic.asText(slice.primary.description)"
					:field="slice.primary.description"
					wrapper="div"
					class="es-video-highlights__intro__description"
				/>
			</div>
			<div class="es-video-highlights__highlights">
				<div class="es-video-highlights__highlights__video">
					<PrismicEmbed
						class="es-video-highlights__highlights__video__embed"
						:field="activeHighlight.videoSource"
						wrapper="div"
					/>
				</div>
				<ul class="es-video-highlights__highlights__tabs">
					<li
						v-for="(item, index) in slice.items"
						:key="item.videoSource.url"
						class="es-video-highlights__highlights__tab"
						:class="{
							'es-video-highlights__highlights__tab--active':
								activeHighlightIndex === index,
						}"
					>
						<PrismicText
							class="es-video-highlights__highlights__tab__button"
							:class="{
								'es-video-highlights__highlights__tab__button--active':
									activeHighlightIndex === index,
							}"
							:field="item.videoTitle"
							wrapper="button"
							@click="activeHighlightIndex = index"
						/>
					</li>
				</ul>
			</div>
		</div>
	</section>
</template>

<script>
import { getSliceComponentProps } from "@prismicio/vue/components";

export default {
	// The array passed to `getSliceComponentProps` is purely optional and acts as a visual hint for you
	props: getSliceComponentProps(["slice", "index", "slices", "context"]),
	data() {
		return {
			activeHighlightIndex: 0,
		};
	},
	computed: {
		activeHighlight() {
			return this.slice.items[this.activeHighlightIndex];
		},
	},
};
</script>
