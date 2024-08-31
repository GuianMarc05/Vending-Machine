<script setup>
import { ref } from 'vue';

const bill = ref(0);
const owed = ref(0);
const change = ref('');
const showChange = ref(false);
const showCh = ref(false);
const showCom = ref(false);

function getChange(bill, owed) {
	let change = bill - owed;
	let result = [];

	if (change >= 1000) {
		let count = Math.floor(change / 1000);
		change -= count * 1000;
		result.push(`${count} x ₱1000 bill`);
	}
	if (change >= 500) {
		let count = Math.floor(change / 500);
		change -= count * 500;
		result.push(`${count} x ₱500 bill`);
	}
	if (change >= 200) {
		let count = Math.floor(change / 200);
		change -= count * 200;
		result.push(`${count} x ₱200 bill`);
	}
	if (change >= 100) {
		let count = Math.floor(change / 100);
		change -= count * 100;
		result.push(`${count} x ₱100 bill`);
	}
	if (change >= 50) {
		let count = Math.floor(change / 50);
		change -= count * 50;
		result.push(`${count} x ₱50 bill`);
	}
	if (change >= 20) {
		let count = Math.floor(change / 20);
		change -= count * 20;
		result.push(`${count} x ₱20 bill`);
	}
	if (change >= 10) {
		let count = Math.floor(change / 10);
		change -= count * 10;
		result.push(`${count} x ₱10 coin`);
	}
	if (change >= 5) {
		let count = Math.floor(change / 5);
		change -= count * 5;
		result.push(`${count} x ₱5 coin`);
	}
	if (change >= 1) {
		let count = Math.floor(change / 1);
		change -= count * 1;
		result.push(`${count} x ₱1 coin`);
	}

	if ((bill === 0 || bill === '') && (owed === 0 || owed === '')) {
		showCom.value = false;
		result.value = 'Insert bill/payment and item amount.';
		return result.value;
	} else if (bill < owed) {
		showCom.value = false;
		result.value = 'Insufficient amount, please insert more.';
		return result.value;
	} else {
		showCom.value = true;
		showCh.value = result.length > 0;
		return result.length ? result.join('<br>') : 'No change.';
	}
}

function calculateChange() {
	change.value = getChange(bill.value, owed.value);
	showChange.value = true;
}

function reset() {
	bill.value = 0;
	owed.value = 0;
	change.value = '';
	showChange.value = false;
	showCom.value = false;
}
</script>

<template>
	<div class="container">
		<form class="form-container" @submit.prevent="calculateChange">
			<div class="content">
				<h3>Bill inserted:</h3>
				<input type="number" v-model="bill" />
				<h3>Item price:</h3>
				<input type="number" v-model="owed" />
				<div class="btn">
					<button type="submit" id="submit">Submit</button>
					<button type="submit" @click.prevent="reset" id="reset">Reset</button>
				</div>
			</div>
		</form>
		<div class="content-change" v-if="showChange">
			<h1 v-if="showCom">Thank you and enjoy!</h1>
			<h2 v-if="showCh">Here's your change!</h2>
			<h2 id="changeAmount" v-html="change"></h2>
		</div>
	</div>
</template>

<style scoped>
.container {
	margin: 10px;
	display: flex;
	flex-direction: column;
	align-items: left;
	justify-content: left;
}

.content {
	display: flex;
	flex-direction: column;
	gap: 15px;
}

.btn {
	display: flex;
	align-items: center;
	justify-content: space-evenly;
	margin-top: 15px;
}

button {
	height: 30px;
	width: 70px;
	background: transparent;
	border-radius: 10px;
	cursor: pointer;
	transition: transform 0.3s ease, box-shadow 0.3s ease;
}

button:hover {
	transform: scale(1.1); /* Scale button to 110% of its original size */
}

#submit {
	border: 1px solid rgb(125, 240, 110);
	color: rgb(125, 240, 110);
}

#reset {
	border: 1px solid rgb(248, 95, 95);
	color: rgb(248, 95, 95);
}

.content-change {
	display: flex;
	flex-direction: column;
	align-items: left;
	justify-content: left;
	margin-top: 35px;
}

#changeAmount {
	margin-top: 15px;
}

h3 {
	color: rgb(216, 216, 216);
}

h2 {
	color: white;
}

h1 {
	color: rgb(243, 245, 143);
}

input {
	width: 100%;
	height: 5vh;
	padding: 10px;
	background: transparent;
	outline: none;
	border: 1px solid rgba(255, 255, 255, 0.2);
	border-radius: 10px;
	color: white;
}
</style>
