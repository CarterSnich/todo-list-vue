<script setup></script>

<template>
	<li class="todoListItem">
		<input
			type="checkbox"
			:checked="done"
		/>
		<span>
			{{ description }}
			<textarea
				ref="textarea"
				v-bind:class="{ hide: description }"
				@blur="validateInput"
			></textarea>
		</span>
		<button
			type="button"
			@click="deleteTodo"
		>
			&times;
		</button>
	</li>
</template>

<script>
export default {
	props: ["index", "description", "done"],
	methods: {
		validateInput(event) {
			this.$emit("validateInput", event.target.value, this.index);
		},

		deleteTodo() {
			this.$emit("deleteTodo", this.index);
		},
	},

	mounted() {
		this.$refs.textarea.focus();
	},
};
</script>
