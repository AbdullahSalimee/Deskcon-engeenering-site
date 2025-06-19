<script>

	

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
<section id="services" class="bg-primary-700 py-8 md:py-24 px-4 sm:px-6">
  <div class="max-w-4xl mx-auto">
      <div class="text-center mb-8 md:mb-12">
          <h2 class="text-2xl sm:text-3xl font-bold text-primary-500 mb-2">Our Services</h2>
          <div class="w-24 sm:w-32 h-1 bg-primary-900 mx-auto"></div>
      </div>

      <div class="space-y-4 sm:space-y-6">
          {#each services as service, index}
              <div
                  class="bg-primary-500 rounded-lg p-4 sm:p-6 border-2 shadow-lg sm:shadow-xl font-heading shadow-primary-900 transition-all duration-300 hover:shadow-xl sm:hover:shadow-2xl hover:shadow-primary-900/50"
              >
                  <div class="flex items-start gap-3 sm:gap-4">
                      <div class="bg-primary-500 my-auto p-2 sm:p-3 rounded-full border-2 border-primary-900">
                          <svg
                              class="w-5 h-5 sm:w-6 sm:h-6 text-primary-900"
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
                          <h3 class="text-xl sm:text-2xl font-light text-primary-100 mb-1">{service.title}</h3>
                          <p class="text-sm sm:text-base text-primary-700">{service.description}</p>

                          {#if expandedService === index}
                              <div
                                  transition:slide|local
                                  class="mt-3 sm:mt-4 p-3 sm:p-4 bg-primary-300 text-primary-900 rounded-lg border border-primary-900/20 text-sm sm:text-base"
                              >
                                  <p>{service.details}</p>
                              </div>
                          {/if}
                      </div>
                      <button
                          on:click={() => toggleService(index)}
                          class="text-primary-300 hover:text-primary-900 p-1 sm:p-2 transition-transform duration-300 {expandedService ===
                          index
                              ? 'rotate-180'
                              : ''}"
                          aria-label={expandedService === index ? 'Collapse details' : 'Expand details'}
                      >
                          <svg class="w-4 h-4 sm:w-5 sm:h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
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