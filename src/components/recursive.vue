<template>
<div>
	<label>
		type name of new {{ levels[0] }}
		<input v-on:keyup.enter="n($event.target)"/>
	</label>
	<draggable v-bind:class="levels[0]" v-model="real">
		<div v-for="(r, i) in real">
			<label v-on:dblclick="real.splice(real.findIndex(e => e.name === r.name), 1)">
				edit {{ levels[0] }} name
				<input v-model="r.name"/>
			</label>
			<recursive v-if="levels[1]" v-bind:recurse="recurse + '[' + i + '][\'' + levels[0] + '\']'" v-bind:levels="levels.slice(1)"></recursive>
		</div>
	</draggable>
</div>
</template>
<script>
import draggable from 'vuedraggable'
export default {
	name: 'recursive',
	components: {
		draggable
	},
	props: {
		recurse: String,
		levels: Array
	},
	computed: {
		real: {
			get() {
				//console.log('this.$root.$children[0]' + this.recurse);
				return eval('this.$root.$children[0]' + this.recurse);
			},
			set(val) {
				eval('this.$root.$children[0]' + this.recurse + ' = val');
			}
		}
	},
	methods: {
		n(v) {
			//console.log(.boards);
			if(v.value) {
				let obj = { name: v.value };
				obj[this.levels[0]] = [];
				this.real.push(obj);
				v.value = "";
			} else {
				alert("type something");
			}
		}
	}
}
</script>
<style>
</style>