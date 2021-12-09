<template>
	<PrismicLink
		class="button"
		:class="{
			'button--black': variant === 'black',
			'button--green': variant === 'green',
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
	},
};
</script>
