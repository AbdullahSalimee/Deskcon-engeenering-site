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

