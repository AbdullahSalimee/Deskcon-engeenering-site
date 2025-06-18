<script>

import { onMount } from 'svelte';
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