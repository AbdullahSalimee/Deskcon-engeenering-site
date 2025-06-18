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
	
</script>
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