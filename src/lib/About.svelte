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