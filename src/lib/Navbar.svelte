<script>
	// @ts-nocheck

	import { onMount } from 'svelte';
	import { cubicOut } from 'svelte/easing';
	import { fade, slide } from 'svelte/transition';

	export let open = '';
	export let active = '';
	let lastKnownPosition = 0;
	let ticking = false;

	onMount(() => {
		const sectionIds = ['top', 'team', 'projects', 'services', 'contact', 'about', 'vision'];
		const sectionElements = new Map();
		const sectionPositions = new Map();
		const scrollOffset = 150;

		function calculatePositions() {
			sectionIds.forEach((id) => {
				const el = document.getElementById(id);
				if (el) {
					const rect = el.getBoundingClientRect();
					sectionPositions.set(id, {
						top: rect.top + window.scrollY,
						bottom: rect.bottom + window.scrollY,
						height: rect.height
					});
				}
			});
		}

		function updateActiveSection() {
			const scrollPosition = window.scrollY + window.innerHeight / 3; // Check 1/3 down viewport
			let newActive = '';

			if (window.innerHeight + window.scrollY >= document.body.offsetHeight - 5) {
				active = 'contact';
				return;
			}

			if (scrollPosition < 50) {
				active = '';
				return;
			}

			let maxVisibility = 0;
			sectionIds.forEach((id) => {
				const section = sectionPositions.get(id);
				if (section) {
					const visibleTop = Math.max(0, scrollPosition - section.top);
					const visibleBottom = Math.max(
						0,
						section.bottom - (scrollPosition + (window.innerHeight * 2) / 3)
					);
					const visibleHeight = section.height - visibleTop - visibleBottom;
					const visibility = Math.max(0, visibleHeight / section.height);

					if (visibility > maxVisibility) {
						maxVisibility = visibility;
						newActive = id === 'top' ? '' : id;
					}
				}
			});

			if (newActive !== active) {
				active = newActive;
			}
		}

		function scrollToSection(id) {
			const section = sectionPositions.get(id);
			if (section) {
				window.scrollTo({
					top: section.top - scrollOffset,
					behavior: 'smooth'
				});
			}
		}

		function handleScroll() {
			lastKnownPosition = window.scrollY;

			if (!ticking) {
				window.requestAnimationFrame(() => {
					updateActiveSection();
					ticking = false;
				});
				ticking = true;
			}
		}

		calculatePositions();
		window.addEventListener('scroll', handleScroll, { passive: true });
		window.addEventListener('resize', calculatePositions);

		updateActiveSection();

		return {
			scrollToSection: (id) => scrollToSection(id),
			destroy: () => {
				window.removeEventListener('scroll', handleScroll);
				window.removeEventListener('resize', calculatePositions);
			}
		};
	});
</script>

<!-- svelte-ignore a11y_consider_explicit_label -->
<nav
	class="grid grid-cols-2 md:flex w-full p-2 h-fit md:h-20 bg-gradient-to-r from-primary-900 via-primary-900 to-primary-300 sticky top-0 z-50 items-center"
>
	<!-- svelte-ignore a11y_invalid_attribute -->
	<a
		href="/"
		on:click={(e) => {
			e.preventDefault();
			active = '';
			open = '';
			window.scrollTo({ top: 0, behavior: 'smooth' });
			history.pushState(null, '', '/');
		}}
		class="flex-none justify-center place-content-center mx-2 md:mx-12 animate-pulse"
	>
		<img src="./logo.png" alt="" class="w-24" />
	</a>

	<!-- svelte-ignore a11y_consider_explicit_label -->
	<!-- svelte-ignore a11y_missing_attribute -->
	<!-- svelte-ignore a11y_click_events_have_key_events -->
	<!-- svelte-ignore a11y_no_static_element_interactions -->
	<a
		class={`${open ? 'hidden' : 'visible'} md:hidden text-primary-500 ml-auto w-fit h-fit p-2 `}
		on:click={() => (open = 'open')}
	>
		<svg width="32" height="32" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
			<path d="M3 12H21" stroke="currentColor" stroke-width="2" stroke-linecap="round" />
			<path d="M3 6H21" stroke="currentColor" stroke-width="2" stroke-linecap="round" />
			<path d="M3 18H21" stroke="currentColor" stroke-width="2" stroke-linecap="round" />
		</svg>
	</a>

	<!-- svelte-ignore a11y_click_events_have_key_events -->

	<!-- svelte-ignore a11y_no_static_element_interactions -->
	<!-- svelte-ignore a11y_missing_attribute -->
	<a
		class={`${open ? 'visible' : 'hidden'} md:hidden text-primary-500 ml-auto w-fit h-fit p-2`}
		on:click={() => (open = '')}
	>
		<svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
			<path d="M18 6L6 18" stroke="currentColor" stroke-width="2" stroke-linecap="round" />
			<path d="M6 6L18 18" stroke="currentColor" stroke-width="2" stroke-linecap="round" />
		</svg>
	</a>
	{#if open === 'open'}
		<div
			transition:slide={{ duration: 300, y: -50, easing: cubicOut }}
			class="grid w-full h-full md:hidden col-span-2 px-4 justify-center"
		>
			<a
				href="#team"
				on:click={() => (active = 'team')}
				class="hover:bg-primary-300 py-2 md:py-0 rounded-2xl md:rounded-none hover:px-6 px-3 text-primary-500 font-heading place-content-center h-full border-primary-300 md:border-l-2 md:border-r duration-300 ease-in-out"
				class:border-b-2={active === 'team'}
			>
				Our Team
			</a>
			<a
				href="#projects"
				on:click={() => (active = 'projects')}
				class=" px-3 text-primary-500 hover:bg-primary-300 py-2 md:py-0 rounded-2xl md:rounded-none hover:px-6 font-heading place-content-center h-full border-primary-300 md:border-l md:border-r duration-300 ease-in-out"
				class:border-b-2={active === 'projects'}
			>
				Projects
			</a>
			<a
				href="#services"
				on:click={() => (active = 'services')}
				class=" px-3 text-primary-500 font-heading hover:bg-primary-300 py-2 md:py-0 rounded-2xl md:rounded-none hover:px-6 place-content-center h-full border-primary-300 md:border-l md:border-r duration-300 ease-in-out"
				class:border-b-2={active === 'services'}
			>
				Services
			</a>
			<a
				href="#vision"
				on:click={() => (active = 'vision')}
				class=" px-3 text-primary-500 font-heading place-content-center h-full hover:bg-primary-300 py-2 md:py-0 rounded-2xl md:rounded-none hover:px-6 border-primary-300 md:border-l md:border-r duration-300 ease-in-out"
				class:border-b-2={active === 'vision'}
			>
				V & M
			</a>
			<a
				href="#about"
				on:click={() => (active = 'about')}
				class=" px-3 text-primary-500 font-heading hover:bg-primary-300 py-2 md:py-0 rounded-2xl md:rounded-none hover:px-6 place-content-center h-full border-primary-300 md:border-l md:border-r-2 duration-300 ease-in-out"
				class:border-b-2={active === 'about'}
			>
				About Us
			</a>
			<a
				href="#contact"
				on:click={() => (active = 'contact')}
				class=" md:ml-auto px-3 text-primary-500 font-heading place-content-center hover:bg-primary-300 py-2 md:py-0 rounded-2xl md:rounded-none hover:px-6 h-full border-primary-300 md:border-l-2 md:border-r-2 duration-300 ease-in-out"
				class:border-b-2={active === 'contact'}
			>
				contact
			</a>
		</div>
	{/if}

	<div class="md:flex grow items-center w-full h-full hidden">
		<a
			href="#team"
			on:click={() => (active = 'team')}
			class="hover:bg-primary-300 py-2 md:py-0 rounded-2xl md:rounded-none hover:px-6 px-3 text-primary-500 font-heading place-content-center h-full border-primary-300 md:border-l-2 md:border-r duration-300 ease-in-out"
			class:border-b-2={open === 'open'}
			class:bg-primary-300={active === 'team'}
			class:px-6={active === 'team'}
		>
			Our Team
		</a>
		<a
			href="#projects"
			on:click={() => (active = 'projects')}
			class=" px-3 text-primary-500 hover:bg-primary-300 py-2 md:py-0 rounded-2xl md:rounded-none hover:px-6 font-heading place-content-center h-full border-primary-300 md:border-l md:border-r duration-300 ease-in-out"
			class:border-b-2={open === 'open'}
			class:bg-primary-300={active === 'projects'}
			class:px-6={active === 'projects'}
		>
			Projects
		</a>
		<a
			href="#services"
			on:click={() => (active = 'services')}
			class=" px-3 text-primary-500 font-heading hover:bg-primary-300 py-2 md:py-0 rounded-2xl md:rounded-none hover:px-6 place-content-center h-full border-primary-300 md:border-l md:border-r duration-300 ease-in-out"
			class:border-b-2={open === 'open'}
			class:bg-primary-300={active === 'services'}
			class:px-6={active === 'services'}
		>
			Services
		</a>
		<a
			href="#vision"
			on:click={() => (active = 'vision')}
			class=" px-3 text-primary-500 font-heading place-content-center h-full hover:bg-primary-300 py-2 md:py-0 rounded-2xl md:rounded-none hover:px-6 border-primary-300 md:border-l md:border-r duration-300 ease-in-out"
			class:border-b-2={open === 'open'}
			class:bg-primary-300={active === 'vision'}
			class:px-6={active === 'vision'}
		>
			V & M
		</a>
		<a
			href="#about"
			on:click={() => (active = 'about')}
			class=" px-3 text-primary-500 font-heading hover:bg-primary-300 py-2 md:py-0 rounded-2xl md:rounded-none hover:px-6 place-content-center h-full border-primary-300 md:border-l border-r-2 duration-300 ease-in-out"
			class:border-b-2={open === 'open'}
			class:bg-primary-300={active === 'about'}
			class:px-6={active === 'about'}
		>
			About Us
		</a>
		<a
			href="#contact"
			on:click={() => (active = 'contact')}
			class=" ml-auto px-3 text-primary-500 font-heading place-content-center hover:bg-primary-900 py-2 md:py-0 rounded-2xl md:rounded-none hover:px-6 h-full border-primary-900 md:border-l-2 border-r-2 duration-300 ease-in-out"
			class:border-b-2={open === 'open'}
			class:bg-primary-900={active === 'contact'}
			class:px-6={active === 'contact'}
		>
			contact
		</a>
	</div>
</nav>
