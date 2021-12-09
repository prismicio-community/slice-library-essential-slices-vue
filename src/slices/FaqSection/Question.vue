<template>
	<div class="faq-section__question">
		<button class="faq-section__question__toggler" @click="isOpen = !isOpen">
			<PrismicText
				:field="title"
				wrapper="span"
				class="faq-section__question__toggler__label"
			/>
			<ChevronIcon
				:direction="isOpen ? 'up' : 'down'"
				:aria-hidden="true"
				class="faq-section__question__toggler__icon"
			/>
		</button>
		<PrismicRichText
			:field="text"
			wrapper="div"
			class="faq-section__question__content"
			:class="{
				'faq-section__question__content--open': isOpen,
			}"
		/>
	</div>
</template>

<script>
import ChevronIcon from "../../components/ChevronIcon.vue";

export default {
	components: {
		ChevronIcon,
	},
	props: {
		title: {
			type: Object,
			required: true,
		},
		text: {
			type: Object,
			required: true,
		},
	},
	data() {
		return {
			isOpen: false,
		};
	},
};
</script>
