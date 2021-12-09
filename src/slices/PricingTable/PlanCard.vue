<template>
	<div
		class="plan-card"
		:class="{
			'plan-card--white': variant === 'white',
			'plan-card--beige': variant === 'beige',
		}"
	>
		<div class="plan-card__content">
			<PrismicText
				v-if="$prismic.asText(title)"
				:field="title"
				wrapper="h3"
				class="plan-card__content__title"
			/>
			<PrismicText
				v-if="$prismic.asText(priceOption)"
				:field="priceOption"
				wrapper="p"
				class="plan-card__content__price"
			/>
			<PrismicRichText
				v-if="$prismic.asText(features)"
				:field="features"
				wrapper="div"
				class="plan-card__content__features"
			/>
		</div>
		<ButtonLink :field="callToAction" class="plan-card__button">
			{{ $prismic.asText(callToActionText) || "Learn more…" }}
		</ButtonLink>
	</div>
</template>

<script>
import ButtonLink from "../../components/ButtonLink.vue";

export default {
	components: {
		ButtonLink,
	},
	props: {
		variant: {
			type: String,
			default: "beige",
			validator: (value) => ["white", "beige"].includes(value),
		},
		title: {
			type: Array,
			required: true,
		},
		priceOption: {
			type: Array,
			required: true,
		},
		features: {
			type: Array,
			required: true,
		},
		callToAction: {
			type: Object,
			required: true,
		},
		callToActionText: {
			type: Array,
			required: true,
		},
	},
};
</script>
