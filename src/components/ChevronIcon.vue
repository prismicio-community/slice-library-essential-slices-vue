<template>
	<svg
		viewBox="0 0 12 8"
		class="es-chevron-icon"
		:class="{
			'es-chevron-icon--up': direction === 'up',
			'es-chevron-icon--down': direction === 'down',
			'es-chevron-icon--left': direction === 'left',
			'es-chevron-icon--right': direction === 'right',
		}"
	>
		<g fill="none">
			<path fill="currentColor" d="M1.41.59 6 5.17 10.59.59 12 2 6 8 0 2z" />
			<path d="M-6-8h24v24H-6z" />
		</g>
	</svg>
</template>

<script>
export default {
	props: {
		direction: {
			type: String,
			required: true,
			validator: (value) => ["up", "down", "left", "right"].includes(value),
		},
	},
};
</script>
