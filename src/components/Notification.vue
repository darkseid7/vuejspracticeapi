<template lang="pug">
	.container 
		.columns
			.column.is-4.is-offset-4
				.notification.is-danger
					slot(name="error") 
	
						
</template>

<style lang="scss" scoped>
	.notification {
		margin: 10px;
		text-align: center;
		font-size: 24px;
	}
</style>
