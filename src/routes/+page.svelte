<script>
	import { onMount } from 'svelte';
	import Navbar from '$lib/Navbar.svelte';
    import Home from '$lib/Home.svelte';

	let active = '';


	onMount(() => {
  const sectionIds = ['top', 'team', 'projects', 'services', 'contact', 'about', 'vision'];
  const visibleSections = new Map();

  // Track if we're at the bottom of the page
  let isAtBottom = false;

  function checkVisibleSections() {
    // If we're at the bottom, force highlight contact
    if (isAtBottom) {
      active = 'contact';
      return;
    }

    // Otherwise find the first visible section
    for (const id of sectionIds) {
      if (visibleSections.get(id)) {
        active = id === 'top' ? '' : id;
        break;
      }
    }
  }

  function handleScroll() {
    const scrollTop = window.scrollY;
    const scrollBottom = scrollTop + window.innerHeight;
    const pageHeight = document.documentElement.scrollHeight;
    
    // Check if we're at the bottom (with 5px threshold)
    isAtBottom = Math.abs(scrollBottom - pageHeight) < 5;

    // Check if we're at the top
    if (scrollTop < 50) {
      active = '';
      return;
    }

    checkVisibleSections();
  }

  // Set up scroll event listener
  window.addEventListener('scroll', handleScroll, { passive: true });

  // Set up IntersectionObserver
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        visibleSections.set(entry.target.id, entry.isIntersecting);
      });
      handleScroll(); // Re-check after visibility changes
    },
    { 
      threshold: 0.5,
      rootMargin: '-30px 0px 0px 0px' // Adjust for fixed header
    }
  );

  // Observe all sections
  sectionIds.forEach((id) => {
    const el = document.getElementById(id);
    if (el) observer.observe(el);
  });

  // Initial check
  handleScroll();

  return () => {
    window.removeEventListener('scroll', handleScroll);
    observer.disconnect();
    // @ts-ignore
    clearInterval(autoSlide); // Clean up the slideshow interval
  };
});
	const equipment = [
		{
			title: 'Columns',
			image: 'column.jpg'
		},
		{
			title: 'Pressure Vessels',
			image: 'reactor.png'
		},
		{
			title: 'Reactor',
			image: 'reactor.jpg'
		},
		{
			title: 'Fractionate Tower',
			image: 'vessel.jpg'
		},
		{
			title: 'Drums and Separators',
			image: 'drum.jpg'
		},
		{
			title: 'LPG Tanks & Bullets',
			image: 'bullet.jpg'
		},
		{
			title: 'Shell & Tube Heat Exchangers',
			image: 'shell.jpg'
		},
		{
			title: 'Atmospheric Storage Tanks',
			image: 'tanks.jpg'
		},
		{
			title: 'Stairways for Storage Tanks',
			image: 'stair.jpg'
		},
		{
			title: 'Platform and Ladders for vessels',
			image: 'plat.jpg'
		},
		{
			title: 'Skid Mounted Packages',
			image: 'skid.jpg'
		},
		{
			title: 'Fire Water Sprinkler Systems',
			image: 'sprink.jpg'
		}
	];

	let currentTeamIndex = 0;

	const teamMembers = [
		{
			name: 'John Smith',
			position: 'Lead Engineer',
			image: 'https://randomuser.me/api/portraits/men/32.jpg'
		},
		{
			name: 'Sarah Johnson',
			position: 'Project Manager',
			image: 'https://randomuser.me/api/portraits/women/44.jpg'
		},
		{
			name: 'Michael Chen',
			position: 'Structural Specialist',
			image: 'https://randomuser.me/api/portraits/men/22.jpg'
		},
		{
			name: 'Emily Rodriguez',
			position: 'CAD Designer',
			image: 'https://randomuser.me/api/portraits/women/63.jpg'
		},
		{
			name: 'David Wilson',
			position: 'Quality Control',
			image: 'https://randomuser.me/api/portraits/men/52.jpg'
		}
	];

	function nextTeamMember() {
		currentTeamIndex = (currentTeamIndex + 1) % teamMembers.length;
	}

	function prevTeamMember() {
		currentTeamIndex = (currentTeamIndex - 1 + teamMembers.length) % teamMembers.length;
	}

	// Auto-rotate every 5 seconds
	onMount(() => {
		const interval = setInterval(nextTeamMember, 3000);
		return () => clearInterval(interval);
	});

	import { slide } from 'svelte/transition';
	/**
	 * @type {number | null}
	 */
	let expandedService = null;

	const services = [
		{
			title: 'Mechanical Equipment Design',
			description:
				'Precise and cost effective engineering solutions for mechanical equipment design.',
			details:
				'We specialize in pressure vessels, heat exchangers, and storage tanks following ASME and API standards.',
			icon: 'M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4'
		},
		{
			title: 'Civil/Structural Design',
			description: 'Innovative design for buildings and industrial infrastructure.',
			details:
				'Our structural solutions include seismic analysis and foundation design using latest industry codes.',
			icon: 'M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4'
		},
		{
			title: 'Electrical & Instrumentation',
			description: 'Comprehensive design for electrical systems.',
			details:
				'We design power distribution, lighting, and control systems compliant with IEC and NEC standards.',
			icon: 'M13 10V3L4 14h7v7l9-11h-7z'
		}
	];

	/**
	 * @param {number | null} index
	 */
	function toggleService(index) {
		expandedService = expandedService === index ? null : index;
	}
</script>
<link rel="shortcut icon" href="favicon.png" type="image/x-icon">
<link
	href="https://fonts.googleapis.com/css2?family=Inter&family=Poppins&family=Roboto&display=swap"
	rel="stylesheet"
/>

<div class="w-full h-full bg-primary-900">
	

	<Navbar />

	<Home />
	

	<section class="bg-primary-700 text-primary-500 py-20 px-4 md:px-16">
		<div class="max-w-7xl mx-auto grid lg:grid-cols-2 gap-10 items-center">
			<div>
				<h1 class="text-4xl md:text-5xl font-bold mb-6 leading-tight">
					Mechanical Equipment Design &<br />Detail Engineering
				</h1>
				<p class="text-lg text-lightBlue mb-4 leading-relaxed">
					Techline Design & Engineering Services provides reliable Basic Design & Detail Engineering
					services for mechanical equipment, using global standards such as <span
						class="font-semibold">API 650/620, ASME Sec. VIII</span
					>, and <span class="font-semibold">TEMA</span>.
				</p>
				<p class="text-lg text-lightBlue mb-4 leading-relaxed">
					We use tools like <span class="font-semibold">PV Elite, HTRI,</span> and
					<span class="font-semibold">AutoCAD</span>
					to ensure accuracy and performance. Our team aligns with global oil and gas leaders like
					<span class="font-semibold">Saudi Aramco, Adnoc, JGC, Shell, Chevron</span>, and more.
				</p>
				<p class="text-lg text-lightBlue mb-4 leading-relaxed">
					With a client-focused approach and deep industry expertise, we tackle complex challenges
					with innovative, precise solutions that exceed expectations.
				</p>
			</div>

			<div class="rounded-xl overflow-hidden shadow-2xl shadow-primary-300 animate-pulse">
				<img
					src="home.jpg"
					alt="Engineering Illustration"
					class="w-full h-[400px] object-cover brightness-70"
				/>
			</div>
		</div>
	</section>

	<section class="bg-primary-500 py-16 px-4 md:px-16" id="top">
		<div class="max-w-7xl mx-auto">
			<h2 class="text-3xl font-semibold mb-6">We Specialize In</h2>

			<div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
				{#each equipment as item}
					<div
						class="p-6 border text-primary-500 border-mediumBlue/20 rounded-xl shadow-2xl shadow-neutral-950 bg-primary-900 hover:shadow-md transition"
					>
						<div class="text-xl font-medium mb-2">{item.title}</div>
						<img
							src={item.image}
							alt={item.title}
							class="rounded-md h-40 w-full object-cover mt-2"
						/>
					</div>
				{/each}
			</div>
		</div>
	</section>

	<section id="team" class="bg-primary-900 py-8 px-4 md:px-16 relative">
		<div class="w-1/2 mx-auto">
			<h2 class="text-4xl font-bold my-12 text-primary-300 text-center">Our Team</h2>

			<div class="relative overflow-hidden">
				<!-- Team Carousel -->
				<div
					class="flex transition-transform duration-300"
					style="transform: translateX(-{currentTeamIndex * 100}%)"
				>
					{#each teamMembers as member (member.name)}
						<div class="w-full flex-shrink-0 px-4">
							<div class="bg-primary-700 rounded-xl shadow-lg p-6 text-center">
								<img
									src={member.image}
									alt={member.name}
									class="w-32 h-32 rounded-full object-cover mx-auto mb-4 border-4 border-primary-500"
								/>
								<h3 class="text-xl font-semibold text-primary-500">{member.name}</h3>
								<p class="text-primary-300">{member.position}</p>
							</div>
						</div>
					{/each}
				</div>

				<!-- Navigation Arrows -->
				<!-- svelte-ignore a11y_consider_explicit_label -->
				<button
					on:click={prevTeamMember}
					class="absolute left-0 top-1/2 -translate-y-1/2 bg-primary-500 text-primary-300 p-2 rounded-full transition z-10"
				>
					<svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"
						><path
							stroke-linecap="round"
							stroke-linejoin="round"
							stroke-width="2"
							d="M15 19l-7-7 7-7"
						/></svg
					>
				</button>
				<!-- svelte-ignore a11y_consider_explicit_label -->
				<button
					on:click={nextTeamMember}
					class="absolute right-0 top-1/2 -translate-y-1/2 bg-primary-500 text-primary-300 p-2 rounded-full hover:bg-darkBlue transition z-10"
				>
					<svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"
						><path
							stroke-linecap="round"
							stroke-linejoin="round"
							stroke-width="2"
							d="M9 5l7 7-7 7"
						/></svg
					>
				</button>
			</div>

			<!-- Dots Indicator -->
			<div class="flex justify-center mt-6 space-x-2">
				{#each teamMembers as _, index}
					<!-- svelte-ignore a11y_consider_explicit_label -->
					<button
						on:click={() => (currentTeamIndex = index)}
						class="w-3 h-3 rounded-full transition-colors"
						class:bg-primary-300={index === currentTeamIndex}
						class:bg-primary-700={index !== currentTeamIndex}
					></button>
				{/each}
			</div>
		</div>
	</section>

	<section id="projects" class="bg-primary-500 py-20 px-4 md:px-16">
		<div class="max-w-7xl mx-auto">
			<div class="text-center mb-16">
				<h2 class="text-4xl font-bold text-primary-100 mb-4">Our Projects</h2>
				<div class="w-24 h-1 bg-primary-300 mx-auto mb-6"></div>
			</div>

			<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
				<!-- Project Card 1 -->
				<div
					class="bg-primary-800 rounded-xl overflow-hidden shadow-lg transform transition-all duration-300 hover:scale-105 hover:shadow-xl"
				>
					<div class="relative h-48">
						<!-- Project Image -->
						<img src="front.jpg" alt="Refinery Project" class="w-full h-full object-cover" />

						<!-- SVG Overlay -->
						<div class="absolute inset-0 bg-primary-900/50 flex items-center justify-center">
							<svg
								class="w-20 h-20 text-primary-300"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="1.5"
									d="M9 17v-2m3 2v-4m3 4v-6m2 10H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"
								></path>
							</svg>
						</div>
					</div>
					<div class="p-6">
						<h3 class="text-xl font-semibold text-primary-100 mb-2">Refinery Upgrade</h3>
						<p class="text-primary-300 italic">Coming Soon</p>
					</div>
				</div>

				<!-- Project Card 2 -->
				<div
					class="bg-primary-800 rounded-xl overflow-hidden shadow-lg transform transition-all duration-300 hover:scale-105 hover:shadow-xl"
				>
					<div class="relative h-48">
						<img src="front2.png" alt="Storage Facility" class="w-full h-full object-cover" />

						<div class="absolute inset-0 bg-primary-900/50 flex items-center justify-center">
							<svg
								class="w-20 h-20 text-primary-300"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="1.5"
									d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4"
								></path>
							</svg>
						</div>
					</div>
					<div class="p-6">
						<h3 class="text-xl font-semibold text-primary-100 mb-2">Storage Facility</h3>
						<p class="text-primary-300 italic">Coming Soon</p>
					</div>
				</div>

				<!-- Project Card 3 -->
				<div
					class="bg-primary-800 rounded-xl overflow-hidden shadow-lg transform transition-all duration-300 hover:scale-105 hover:shadow-xl"
				>
					<div class="relative h-48">
						<img src="front3.png" alt="Power Plant" class="w-full h-full object-cover" />

						<div class="absolute inset-0 bg-primary-900/50 flex items-center justify-center">
							<svg
								class="w-20 h-20 text-primary-300"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="1.5"
									d="M13 10V3L4 14h7v7l9-11h-7z"
								></path>
							</svg>
						</div>
					</div>
					<div class="p-6">
						<h3 class="text-xl font-semibold text-primary-100 mb-2">Power Plant</h3>
						<p class="text-primary-300 italic">Coming Soon</p>
					</div>
				</div>
			</div>

			<div class="text-center mt-16">
				<p class="text-primary-200 text-lg italic max-w-3xl mx-auto">
					We're currently finalizing our project documentation. Detailed case studies with
					specifications, challenges, and our engineering solutions will be added to the website
					soon.
				</p>
				<button
					class="mt-8 px-8 py-3 bg-primary-300 text-primary-900 font-semibold rounded-full hover:bg-primary-200 transition duration-300"
				>
					Notify Me When Available
					<svg class="w-4 h-4 inline ml-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
						<path
							stroke-linecap="round"
							stroke-linejoin="round"
							stroke-width="2"
							d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
						></path>
					</svg>
				</button>
			</div>
		</div>
	</section>

	<!-- ! Sevvices -->

	<section id="services" class="bg-primary-700 py-16 px-4">
		<div class="max-w-4xl mx-auto">
			<div class="text-center mb-12">
				<h2 class="text-3xl font-bold text-primary-500 mb-2">Our Services</h2>
				<div class="w-32 h-1 bg-primary-900 mx-auto"></div>
			</div>

			<div class="space-y-6">
				{#each services as service, index}
					<div
						class="bg-primary-500 rounded-lg p-6 border-2 shadow-xl font-heading shadow-primary-900 transition-all duration-300 hover:shadow-2xl hover:shadow-primary-900/50"
					>
						<div class="flex items-start gap-4">
							<div class="bg-primary-500 my-auto p-3 rounded-full border-2 border-primary-900">
								<svg
									class="w-6 h-6 text-primary-900"
									fill="none"
									stroke="currentColor"
									viewBox="0 0 24 24"
								>
									<path
										stroke-linecap="round"
										stroke-linejoin="round"
										stroke-width="1.5"
										d={service.icon}
									></path>
								</svg>
							</div>
							<div class="flex-1">
								<h3 class="text-2xl font-light text-primary-100 mb-1">{service.title}</h3>
								<p class="text-primary-700">{service.description}</p>

								{#if expandedService === index}
									<div
										transition:slide|local
										class="mt-4 p-4 bg-primary-300 text-primary-900 rounded-lg border border-primary-900/20"
									>
										<p>{service.details}</p>
									</div>
								{/if}
							</div>
							<button
								on:click={() => toggleService(index)}
								class="text-primary-300 hover:text-primary-900 p-2 transition-transform duration-300 {expandedService ===
								index
									? 'rotate-180'
									: ''}"
								aria-label={expandedService === index ? 'Collapse details' : 'Expand details'}
							>
								<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
									<path
										stroke-linecap="round"
										stroke-linejoin="round"
										stroke-width="2"
										d="M19 9l-7 7-7-7"
									></path>
								</svg>
							</button>
						</div>
					</div>
				{/each}
			</div>
		</div>
	</section>
	<!-- ! V&M -->
	<section
		id="vision"
		class="relative py-24 px-4 bg-gradient-to-br from-primary-900 to-primary-800"
	>
		<!-- Geometric background pattern -->
		<div class="absolute inset-0 opacity-10">
			<div
				class="absolute inset-0 bg-[url('data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxyZWN0IHdpZHRoPSIxMDAiIGhlaWdodD0iMTAwIiBmaWxsPSJub25lIiBzdHJva2U9IiNmZmYiIHN0cm9rZS13aWR0aD0iMSIgb3BhY2l0eT0iMC4xIi8+PC9zdmc+')]"
			></div>
		</div>

		<div class="max-w-6xl mx-auto relative z-10">
			<!-- Section header -->
			<div class="text-center mb-16">
				<h2 class="text-5xl font-bold text-white mb-4">
					<span class="text-primary-500">Our</span> Purpose
				</h2>
				<div class="w-32 h-1 bg-primary-500 mx-auto"></div>
			</div>

			<!-- Vision & Mission cards -->
			<div class="grid md:grid-cols-2 gap-10">
				<!-- Vision Card -->
				<div
					class="bg-primary-800/50 backdrop-blur-sm rounded-3xl p-10 border border-primary-700 hover:border-primary-500 transition-all duration-500 hover:shadow-xl hover:shadow-primary-500/10"
				>
					<div class="flex items-center mb-6">
						<div class="bg-primary-500 p-3 rounded-lg mr-4">
							<svg
								class="w-8 h-8 text-primary-900"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="1.5"
									d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"
								/>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="1.5"
									d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"
								/>
							</svg>
						</div>
						<h3 class="text-3xl font-bold text-white">Vision</h3>
					</div>
					<div class="space-y-6">
						<p class="text-primary-300 text-lg leading-relaxed">
							"This is a simple idea with massive profundity, which shall keep us resolute and
							persistent to serve the humanity by creating a collaborative culture, one that is
							primed to seize every opportunity and transform it into success."
						</p>
						<div class="flex items-center space-x-3">
							<div class="w-8 h-0.5 bg-primary-500"></div>
							<span class="text-primary-500 font-medium">Forward Thinking</span>
						</div>
					</div>
				</div>

				<!-- Mission Card -->
				<div
					class="bg-primary-800/50 backdrop-blur-sm rounded-3xl p-10 border border-primary-700 hover:border-primary-500 transition-all duration-500 hover:shadow-xl hover:shadow-primary-500/10"
				>
					<div class="flex items-center mb-6">
						<div class="bg-primary-500 p-3 rounded-lg mr-4">
							<svg
								class="w-8 h-8 text-primary-900"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="1.5"
									d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z"
								/>
							</svg>
						</div>
						<h3 class="text-3xl font-bold text-white">Mission</h3>
					</div>
					<div class="space-y-6">
						<ul class="space-y-4 text-primary-300 text-lg">
							<li class="flex items-start">
								<svg
									class="w-5 h-5 text-primary-500 mr-3 mt-0.5 flex-shrink-0"
									fill="none"
									stroke="currentColor"
									viewBox="0 0 24 24"
								>
									<path
										stroke-linecap="round"
										stroke-linejoin="round"
										stroke-width="2"
										d="M5 13l4 4L19 7"
									/>
								</svg>
								<span
									>"To establish an organization of individuals passionately committed to
									excellence"</span
								>
							</li>
							<li class="flex items-start">
								<svg
									class="w-5 h-5 text-primary-500 mr-3 mt-0.5 flex-shrink-0"
									fill="none"
									stroke="currentColor"
									viewBox="0 0 24 24"
								>
									<path
										stroke-linecap="round"
										stroke-linejoin="round"
										stroke-width="2"
										d="M5 13l4 4L19 7"
									/>
								</svg>
								<span>"Innovative solutions with reliable safety and quality"</span>
							</li>
							<li class="flex items-start">
								<svg
									class="w-5 h-5 text-primary-500 mr-3 mt-0.5 flex-shrink-0"
									fill="none"
									stroke="currentColor"
									viewBox="0 0 24 24"
								>
									<path
										stroke-linecap="round"
										stroke-linejoin="round"
										stroke-width="2"
										d="M5 13l4 4L19 7"
									/>
								</svg>
								<span>"Value relationships and remain fair in all dealings"</span>
							</li>
						</ul>
						<div class="flex items-center space-x-3">
							<div class="w-8 h-0.5 bg-primary-500"></div>
							<span class="text-primary-500 font-medium">Core Values</span>
						</div>
					</div>
				</div>
			</div>

			<!-- Decorative footer -->
			<div class="mt-20 text-center">
				<div
					class="inline-block px-6 py-3 bg-primary-500/10 border border-primary-500/30 rounded-full"
				>
					<span class="text-primary-300">Engineering Excellence •</span>
					<span class="text-primary-500 mx-2">Innovation •</span>
					<span class="text-primary-300">Collaboration</span>
				</div>
			</div>
		</div>
	</section>
	<!-- ! about -->
	<section id="about" class="relative py-28 px-4 bg-primary-500 overflow-hidden">
		<!-- Decorative elements -->
		<div class="absolute top-0 left-0 w-full h-full opacity-5">
			<div
				class="absolute top-1/4 -left-20 w-80 h-80 bg-[#0080ff] rounded-full filter blur-3xl"
			></div>
			<div
				class="absolute bottom-1/3 -right-20 w-64 h-64 bg-[#008cef] rounded-full filter blur-3xl"
			></div>
		</div>

		<div class="max-w-7xl mx-auto relative z-10">
			<!-- Section header with diagonal accent -->
			<div class="relative mb-20 pl-6 md:pl-12">
				<div
					class="absolute left-0 top-0 bottom-0 w-1 bg-gradient-to-b from-[#000000] to-pritext-primary-300 transform -skew-x-12"
				></div>
				<h2 class="text-5xl font-bold text-primary-300">
					<span class="text-primary-900">About</span> Techline
				</h2>
				<p class="text-primary-700 mt-2">Design & Engineering Services</p>
			</div>

			<!-- Content grid -->
			<div class="grid lg:grid-cols-2 gap-16 items-center">
				<!-- Left column - Image with overlay text -->
				<div class="relative group">
					<div
						class="relative aspect-[4/3] bg-primary-800 rounded-xl overflow-hidden shadow-2xl shadow-primary-900"
					>
						<img
							src="home.jpg"
							alt="Engineering team working"
							class="w-full h-full object-cover transform group-hover:scale-105 transition duration-700 "
						/>
						<div
							class="absolute inset-0 bg-gradient-to-t from-primary-900/90 via-primary-900/40 to-transparent"
						></div>
						<div class="absolute bottom-0 left-0 p-8">
							<div class="text-primary-900 font-bold text-lg">SINCE 2023</div>
							<div class="text-white text-2xl font-bold">Engineering Excellence</div>
						</div>
					</div>
				</div>

				<!-- Right column - Text content -->
				<div class="space-y-8">
					<div class="prose prose-lg max-w-none text-primary-900">
						<p class="text-xl leading-relaxed">
							Techline Design & Engineering Services is a multidisciplinary engineering company
							specializing in Mechanical, Civil, and Electrical projects, with particular focus on
							the oil and gas sector.
						</p>
						<p class="leading-relaxed">
							Our team of highly skilled professionals delivers comprehensive designs, ensuring
							every project is executed with precision. From Front-End Engineering Design to
							detailed engineering, we maintain excellence across all aspects of mechanical,
							civil/structural, and electrical design.
						</p>
						<div class="relative pl-6 my-6 border-l-4 border-primary-900">
							<p class="italic text-primary-300 font-medium">
								"We don't just meet expectations - we redefine them through innovative engineering
								solutions."
							</p>
						</div>
						<p class="leading-relaxed">
							Our commitment to client satisfaction and tailored approach sets us apart. We
							understand our clients' unique challenges and add significant value at every project
							stage. With a proven track record, we build long-term partnerships based on trust,
							reliability, and exceptional performance.
						</p>
					</div>

					<!-- Specializations -->
					<div class="grid sm:grid-cols-2 gap-4 mt-8">
						<div
							class="bg-primary-800/50 p-4 shadow-2xl rounded-lg border-2 border-primary-300 flex items-center"
						>
							<svg
								class="w-6 h-6 text-primary-700 mr-3 flex-shrink-0"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="1.5"
									d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4"
								></path>
							</svg>
							<span class="text-primary-900">Mechanical Design</span>
						</div>
						<div
							class="bg-primary-800/50 p-4 shadow-2xl rounded-lg border-2 border-primary-300 flex items-center"
						>
							<svg
								class="w-6 h-6 text-primary-700 mr-3 flex-shrink-0"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="1.5"
									d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4"
								></path>
							</svg>
							<span class="text-primary-900">Civil/Structural</span>
						</div>
						<div
							class="bg-primary-800/50 p-4 shadow-2xl rounded-lg border-2 border-primary-300 flex items-center"
						>
							<svg
								class="w-6 h-6 text-primary-700 mr-3 flex-shrink-0"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="1.5"
									d="M13 10V3L4 14h7v7l9-11h-7z"
								></path>
							</svg>
							<span class="text-primary-900">Electrical Systems</span>
						</div>
						<div
							class="bg-primary-800/50 p-4 shadow-2xl rounded-lg border-2 border-primary-300 flex items-center"
						>
							<svg
								class="w-6 h-6 text-primary-700 mr-3 flex-shrink-0"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="1.5"
									d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z"
								></path>
							</svg>
							<span class="text-primary-900">Oil & Gas Specialists</span>
						</div>
					</div>
				</div>
			</div>

			<!-- Stats bar -->
			<div class="grid md:grid-cols-4 gap-6 mt-20">
				<div class="text-center">
					<div class="text-4xl font-bold text-primary-900 mb-2">50+</div>
					<div class="text-primary-300">Projects Completed</div>
				</div>
				<div class="text-center">
					<div class="text-4xl font-bold text-primary-900 mb-2">100%</div>
					<div class="text-primary-300">Client Satisfaction</div>
				</div>
				<div class="text-center">
					<div class="text-4xl font-bold text-primary-900 mb-2">24/7</div>
					<div class="text-primary-300">Support</div>
				</div>
				<div class="text-center">
					<div class="text-4xl font-bold text-primary-900 mb-2">10+</div>
					<div class="text-primary-300">Years Combined Experience</div>
				</div>
			</div>
		</div>
	</section>

	<!-- ! contact -->
	<section id="contact" class="relative py-28 px-4 bg-primary-900 overflow-hidden">
		<!-- Decorative blur elements -->
		<div class="absolute top-0 left-0 w-full h-full opacity-5">
			<div
				class="absolute top-1/4 -left-20 w-80 h-80 bg-primary-300 rounded-full filter blur-3xl"
			></div>
			<div
				class="absolute bottom-1/3 -right-20 w-64 h-64 bg-primary-700 rounded-full filter blur-3xl"
			></div>
		</div>

		<div class="max-w-7xl mx-auto relative z-10">
			<!-- Section header -->
			<div class="relative mb-20 pl-6 md:pl-12">
				<div
					class="absolute left-0 top-0 bottom-0 w-1 bg-gradient-to-b from-primary-500 to-primary-300 transform -skew-x-12"
				></div>
				<h2 class="text-5xl font-bold text-white">
					<span class="text-primary-500">Contact</span> Us
				</h2>
				<p class="text-primary-300 mt-2">Let’s connect and elevate your project to new heights.</p>
			</div>

			<!-- Contact Info Grid -->
			<div class="grid md:grid-cols-2 gap-16 items-start">
				<!-- Left Column - Contact Info -->
				<div class="space-y-8 text-primary-300 prose prose-lg max-w-none">
					<div class="flex items-start gap-4">
						<svg
							class="w-6 h-6 text-primary-500 flex-shrink-0 mt-1"
							fill="none"
							stroke="currentColor"
							viewBox="0 0 24 24"
						>
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="1.5"
								d="M3 5h18M9 3v2m6-2v2m-9 4h12M5 9v10a2 2 0 002 2h10a2 2 0 002-2V9"
							></path>
						</svg>
						<div>
							<h4 class="text-white font-semibold">Phone</h4>
							<p class="leading-relaxed">+92 300 4885588</p>
						</div>
					</div>

					<div class="flex items-start gap-4">
						<svg
							class="w-6 h-6 text-primary-500 flex-shrink-0 mt-1"
							fill="none"
							stroke="currentColor"
							viewBox="0 0 24 24"
						>
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="1.5"
								d="M16 12l-4-4-4 4m8 0l-4 4-4-4"
							></path>
						</svg>
						<div>
							<h4 class="text-white font-semibold">Email</h4>
							<p class="leading-relaxed">info@techline.engineering</p>
						</div>
					</div>

					<div class="flex items-start gap-4">
						<svg
							class="w-6 h-6 text-primary-500 flex-shrink-0 mt-1"
							fill="none"
							stroke="currentColor"
							viewBox="0 0 24 24"
						>
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="1.5"
								d="M17.657 16.657L13.414 12.414a2 2 0 00-2.828 0L6.343 16.657M15 10V6a3 3 0 00-6 0v4"
							></path>
						</svg>
						<div>
							<h4 class="text-white font-semibold">Address</h4>
							<p class="leading-relaxed">
								Garden View Colony, Near Chugtai Lab, Chauk Steel Bagh, Kasur, Pakistan
							</p>
						</div>
					</div>
				</div>

				<!-- Right Column - Contact Card -->
				<div class="bg-primary-700/40 rounded-xl border border-primary-700 p-8 shadow-xl space-y-6">
					<h3 class="text-3xl font-bold text-white">Send us a Message</h3>
					<form class="space-y-4">
						<input
							type="text"
							placeholder="Full Name"
							class="w-full bg-primary-900/60 border border-primary-700 text-primary-900 placeholder-primary-300 rounded-md px-4 py-3 focus:outline-none focus:ring-2 focus:ring-primary-500"
						/>
						<input
							type="email"
							placeholder="Email Address"
							class="w-full bg-primary-900/60 border border-primary-700 text-primary-900 placeholder-primary-300 rounded-md px-4 py-3 focus:outline-none focus:ring-2 focus:ring-primary-500"
						/>
						<textarea
							placeholder="Your Message"
							rows="4"
							class="w-full bg-primary-900/60 border border-primary-700 text-primary-900 placeholder-primary-300 rounded-md px-4 py-3 focus:outline-none focus:ring-2 focus:ring-primary-500"
						></textarea>
						<button
							type="submit"
							class="bg-primary-500 hover:bg-primary-300 text-primary-900 font-semibold px-6 py-3 rounded-md transition duration-300"
						>
							Send Message
						</button>
					</form>
				</div>
			</div>
		</div>
	</section>
</div>

<!-- ? Tailwind css -->

<!-- * Conditonal claseses in tailwind css -->

<!-- 
 <script>
  let toggle = true;
</script>

<button on:click={() =>
toggle = !toggle
  
  }>
  click me
</button>

<div 
class={`${toggle ? 'bg-green-900' : 'bg-red-900'} text-white`}


>
  this is my kindom
</div> -->

<!-- 
 <script>
let check ='';

 </script>

<input type="text" bind:value={check}>
<div class={check.length >= 6 ? "bg-green-900":"bg-red-600" }>writename</div> -->

<!-- 

 
🔸 Common Mistakes to Avoid
❌ Passing variables to a function and modifying only the parameter (doesn’t change original)
❌ Forgetting to directly update reactive variables (let x = y won't trigger reactivity)
❌ Putting logic directly in class="" without using class={} in Svelte/JSX  -->

<!-- ! in TailwindCss -->

<!-- 
<div class="  text-amber-700! text-red-800 text-9xl ">
  This text will be red, not gray.
</div> -->

<!-- ? For migration -->

<!-- 

npx @tailwindcss/upgrade

npx @tailwindcss/upgrade --force 

-->

<!-- * new things -->

<!-- 
<div class="columns-1 p-11 gap-2xl sm:columns-5">
  <img class="aspect-auto " src="./front.jpg" alt="" />
  <img class="aspect-square " src="./logo.png" alt="" />
  <img class="aspect-square " src="./front.jpg" alt="" />

  <img class="aspect-square " src="./front.jpg" alt="" />
  <img class="aspect-square " src="./logo.png" alt="" />
  <img class="aspect-square " src="./front.jpg" alt="" />
  <img class="aspect-3/2 " src="./front.jpg" alt="" />
  <img class="aspect-square " src="./logo.png" alt="" />
  <img class="aspect-square " src="./front.jpg" alt="" />
</div> -->

<!-- break after/before/inside -->

<!-- 
<div class="columns-2">
  <p>Well, let me tell you something, </p>
  <p >Sure, go ahead, laugh</p>
  <p class="break-after-column ">Maybe we can live without</p>
  <p>Look. If you think this is</p>
</div> -->

<!-- <div class="columns-2">
  <p>Well, let me tell you something, </p>
  <p class="break-inside-avoid-column">Sure, go ahead, laugh</p>
  <p>Maybe we can live without</p>
  <p>Look. If you think this is</p>
</div> -->

<!-- <div class="flex items-center p-24">
  <img src="./front.jpg"  alt="" class="w-24 rounded-full"/>
  <div class="px-3  cursor-pointer text-primary-500   font-heading place-content-center h-full  border-primary-300 border-l ">
    <strong>Andrew Alfred</strong>
    <span>Technical advisor</span>
  </div>
</div> -->

<!-- ! Svelte -->

<!-- ? runes -->

<!-- 
<script>
  let counts = [1, 5, 10, 1339, 2048];
</script>

{#each counts as count}
  <div class="px-3  cursor-pointer text-primary-500   font-heading place-content-center h-full  border-primary-300 border-l ">
    Count: {count}, Doubled: {count * 4}
  </div>
{/each}

 -->

<!-- $state -->

<!-- <script>
	let count = $state(0);
</script>

<button  onclick={() => count++} >
	clicks: {count}
</button> -->

<!-- 
<script>


	const todos = $state([
		{
			done: false,
			text: 'add more todos'
		},
		{
			ok: true
		}
	]);



	function toggleOk() {
		todos[1].ok = !todos[1].ok;
	}


</script>

<button onclick={toggleOk}>
	click
</button>

<div class="px-3  cursor-pointer text-primary-500   font-heading place-content-center h-full  border-primary-300 border-l ">
	{todos[1].ok ? 'true' : 'false'}
</div>

 -->
