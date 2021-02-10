<template>
<main class="w-screen h-screen flex overflow-hidden" :class="themePreference">
	<!-- Left section -->
	<div class="w-4/12 bg-warmGray-100 flex justify-end min-w-max pt-14 pb-32 pr-4">
		<div class="w-52 h-full flex-shrink-0">
			<Nav/>
		</div>
	</div>
	<!-- Right section -->
	<div class="w-8/12 bg-green-400 min-w-min">
		<section class="w-8/12 h-full min-w-max bg-pink-600">
		<div class="w-96 h-3"></div>
		</section>
	</div>
</main>
</template>

<script>
export default {

	data() {
		return {
			themePreference: undefined
		}
	},

	methods: {

		chooseThemePreference() {
			// On page load or when changing themes, best to add inline in `head` to avoid FOUC
			if (localStorage.theme === 'dark' || (!('theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
				document.documentElement.classList.add('dark')
			} else {
				document.documentElement.classList.remove('dark')
			}

			// Whenever the user explicitly chooses light mode
			localStorage.theme = 'light'

			// Whenever the user explicitly chooses dark mode
			localStorage.theme = 'dark'

			// Whenever the user explicitly chooses to respect the OS preference
			localStorage.removeItem('theme')
		}

	},

	mounted() {

		if ( process.client ) {

			this.chooseThemePreference()
			this.themePreference = localStorage.theme

		}

	}

}
</script>
