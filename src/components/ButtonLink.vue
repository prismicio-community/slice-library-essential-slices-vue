<template>
	<PrismicLink
		:field="field"
		class="es-button"
		:class="{
			'es-button--black': variant === 'black',
			'es-button--green': variant === 'green',
		}"
	>
		<slot />
	</PrismicLink>
</template>

<script>
export default {
	props: {
		variant: {
			type: String,
			default: "black",
			validator: (value) => ["black", "green"].includes(value),
		},
		field: {
			type: Object,
			required: true,
		},
	},
};
</script>
