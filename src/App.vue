<template>
	<div id="app">
		<label>
			type name of new board and hit enter
			<input v-on:keyup.enter="boards.push({name: $event.target.value, categories: []})"/>
		</label>
		<draggable v-model="boards">
		<div class="board" v-for="board in boards">
			<label>
				edit board name
				<input v-model="board.name"/>
			</label>
			<br>
			<label>
				type name of new category in {{ board.name }}
				<input v-on:keyup.enter="board.categories.push({name: $event.target.value, cards: []})"/>
				<div class="container">
					<draggable v-model="board.categories">
					<div v-for="category in board.categories">
						<label>
							edit category name
							<input v-model="category.name">
						</label>
						<br>
						<label>
							type name of new card in {{ category.name }}
							<input v-on:keyup.enter="category.cards.push({name: $event.target.value})"/>
						</label>
						<draggable v-model="category.cards">
						<div v-for="card in category.cards" v-on:dblclick="category.cards.splice(category.cards.findIndex(element => element.name === card.name), 1)">
							{{ card.name }}
						</div>
						</draggable>
					</div>
					</draggable>
				</div>
			</label>
		</div>
		</draggable>
	</div>
</template>

<script>
import draggable from 'vuedraggable'
export default {
	name: 'app',
	components: {
		draggable
	},
	data: function() {
		return {
			boards: []
		}
	}
}
</script>

<style>
.container > div {
	display: flex;
}
.container > div > div {
	border-style: dotted;
}
.board {
	border-style: groove;
}
</style>
