<template>
	<h1>Suspense Example</h1>
	<div v-if="errMsg">{{ errMsg }}</div>
	<Suspense v-else>
		<template #default><UsersList /></template>
		<template #fallback>
			<div class="lds-ripple">
				<div></div>
				<div></div>
			</div>
		</template>
	</Suspense>
</template>
<script>
import { onErrorCaptured, ref } from 'vue';
import UsersList from './UsersList';
export default {
	components: {
		UsersList,
	},

	setup() {
		const errMsg = ref(null);

		onErrorCaptured(() => {
			errMsg.value = 'Something went wrong';
		});
		return {
			errMsg,
		};
	},
};
</script>

<style>
/* Spinner */

.lds-ripple {
	display: inline-block;
	position: relative;
	width: 80px;
	height: 80px;
	transition-delay: 5s;
	transition-duration: 5s;
}
.lds-ripple div {
	position: absolute;
	border: 4px solid black;
	opacity: 1;
	border-radius: 50%;
	animation: lds-ripple 1s cubic-bezier(0, 0.2, 0.8, 1) infinite;
}
.lds-ripple div:nth-child(2) {
	animation-delay: -0.5s;
}
@keyframes lds-ripple {
	0% {
		top: 36px;
		left: 36px;
		width: 0;
		height: 0;
		opacity: 0;
	}
	4.9% {
		top: 36px;
		left: 36px;
		width: 0;
		height: 0;
		opacity: 0;
	}
	5% {
		top: 36px;
		left: 36px;
		width: 0;
		height: 0;
		opacity: 1;
	}
	100% {
		top: 0px;
		left: 0px;
		width: 72px;
		height: 72px;
		opacity: 0;
	}
}

/* Spinner */
</style>
