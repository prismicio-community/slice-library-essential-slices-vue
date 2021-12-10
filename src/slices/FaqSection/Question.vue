<template>
	<div class="es-faq-section__question">
		<button class="es-faq-section__question__toggler" @click="isOpen = !isOpen">
			<PrismicText
				:field="title"
				wrapper="span"
				class="es-faq-section__question__toggler__label"
			/>
			<ChevronIcon
				:direction="isOpen ? 'up' : 'down'"
				:aria-hidden="true"
				class="es-faq-section__question__toggler__icon"
			/>
		</button>
		<PrismicRichText
			:field="text"
			wrapper="div"
			class="es-faq-section__question__content"
			:class="{
				'es-faq-section__question__content--open': isOpen,
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
			type: Array,
			required: true,
		},
		text: {
			type: Array,
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
