<script>
	const makeCall = () => {
	  window.location.href = 'tel:+923004885588';
	};
  
	const openMaps = () => {
	  const address = encodeURIComponent('Garden View Colony, Near Chugtai Lab, Chauk Steel Bagh, Kasur, Pakistan');
	  window.open(`https://www.google.com/maps/search/?api=1&query=${address}`, '_blank');
	};
  </script>
  
  <section id="contact" class="relative py-28 px-4 overflow-hidden">
	<div class="mx-auto relative z-10 max-w-6xl">
	  <div class="relative mb-20 pl-6 md:pl-12">
		<h2 class="text-5xl font-bold text-white">
		  <span class="text-primary-500">Contact</span> Us
		</h2>
		<p class="text-primary-300 mt-2">Let's connect and elevate your project to new heights.</p>
	  </div>
  
	  <div class="grid md:grid-cols-2 gap-16 items-start">
		<div class="space-y-8 text-primary-300 prose prose-lg max-w-none my-auto">
		  <div class="flex items-start gap-4 group cursor-pointer" on:click={makeCall}>
			<svg
			  class="w-6 h-6 text-primary-500 flex-shrink-0 mt-1 group-hover:text-white transition-colors"
			  fill="none"
			  stroke="currentColor"
			  viewBox="0 0 24 24"
			>
			  <path
				stroke-linecap="round"
				stroke-linejoin="round"
				stroke-width="1.5"
				d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"
			  />
			</svg>
			<div class="group-hover:text-white transition-colors">
			  <h4 class="font-semibold text-white group-hover:text-primary-300 transition-colors">Phone</h4>
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
				d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
			  />
			</svg>
			<div>
			  <h4 class="text-white font-semibold">Email</h4>
			  <p class="leading-relaxed">info@techline.engineering</p>
			</div>
		  </div>
  
		  <div class="flex items-start gap-4 group cursor-pointer" on:click={openMaps}>
			<svg
			  class="w-6 h-6 text-primary-500 flex-shrink-0 mt-1 group-hover:text-white transition-colors"
			  fill="none"
			  stroke="currentColor"
			  viewBox="0 0 24 24"
			>
			  <path
				stroke-linecap="round"
				stroke-linejoin="round"
				stroke-width="1.5"
				d="M17.657 16.657L13.414 12.414a2 2 0 00-2.828 0L6.343 16.657M15 10V6a3 3 0 00-6 0v4"
			  />
			</svg>
			<div class="group-hover:text-white transition-colors">
			  <h4 class="font-semibold text-white group-hover:text-primary-300 transition-colors">Address</h4>
			  <p class="leading-relaxed">
				Garden View Colony, Near Chugtai Lab, Chauk Steel Bagh, Kasur, Pakistan
			  </p>
			</div>
		  </div>
  
		  <button
			on:click={makeCall}
			class="mt-8 px-8 py-3 bg-primary-300 text-primary-900 font-semibold rounded-full hover:bg-primary-200 transition duration-300 inline-flex items-center"
			aria-label="Call us at +92 300 4885588"
		  >
			Call Us Now
			<svg 
			  class="w-5 h-5 ml-2" 
			  fill="none" 
			  stroke="currentColor" 
			  viewBox="0 0 24 24" 
			>
			  <path 
				stroke-linecap="round" 
				stroke-linejoin="round" 
				stroke-width="2" 
				d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"
			  />
			</svg>
		  </button>
		</div>
  
		<div class="rounded-lg overflow-hidden shadow-xl">
		  <img 
			src="front2.png" 
			alt="Techline Engineering Office" 
			class="w-full h-auto object-cover"
			loading="lazy"
		  />
		</div>
	  </div>
	</div>
  </section>