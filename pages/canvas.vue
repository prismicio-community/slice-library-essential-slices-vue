<template>
	<SliceCanvasRenderer v-slot="{ slices }" :state="state">
		<SliceZone
			:slices="slices"
			:resolver="({ sliceName }) => sliceName.replace(/_/g, '-')"
		/>
	</SliceCanvasRenderer>
</template>

<script>
import { SliceCanvasRenderer } from "@prismicio/slice-canvas-renderer-vue";

import state from "~~/.slicemachine/libraries-state.json";

export default {
	components: {
		SliceCanvasRenderer,
	},
	data() {
		return { state };
	},
};
</script>
