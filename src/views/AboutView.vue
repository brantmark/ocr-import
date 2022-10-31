<script setup>
import { createWorker } from 'tesseract.js'
import { onMounted } from 'vue'

const worker = createWorker({
	logger: (m) => console.log(m),
})

// functions
const parse = async () => {
	await worker.load()
	await worker.loadLanguage('eng')
	await worker.initialize('eng')
	const {
		data: { text },
	} = await worker.recognize(
		'https://tesseract.projectnaptha.com/img/eng_bw.png'
	)
	console.log(text)
	await worker.terminate()
}
onMounted(() => parse())
</script>

<template>
	<div class="about">
		<h1>This is an about page</h1>
	</div>
</template>

<style>
@media (min-width: 1024px) {
	.about {
		min-height: 100vh;
		display: flex;
		align-items: center;
	}
}
</style>
