<template>
	<recursive id="app" v-bind:recurse="'.boards'" v-bind:levels="['board', 'category', 'card']"></recursive>
</template>

<script>

import recursive from './components/recursive.vue'
export default {
	name: 'app',
	components: {
		recursive
	},
	data: function() {
		return {
			boards: []
		}
	}
}
</script>

<style>
.category {
	display: flex;
}
.category > div {
	border-style: dotted;
}
.card {
	border-style: outset;
}
.card > div {
	border-style: double;
}
.board > div {
	border-style: groove;
}
</style>
