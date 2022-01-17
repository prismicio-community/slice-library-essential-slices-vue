<template>
	<SliceSimulator v-slot="{ slices }" :state="state">
		<SliceZone
			:slices="slices"
			:resolver="({ sliceName }) => sliceName.replace(/_/g, '-')"
		/>
	</SliceSimulator>
</template>

<script>
import { SliceSimulator } from "@prismicio/slice-simulator-vue";

import state from "~~/.slicemachine/libraries-state.json";

export default {
	components: {
		SliceSimulator,
	},
	data() {
		return { state };
	},
};
</script>
