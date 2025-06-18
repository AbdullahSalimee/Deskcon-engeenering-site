<script>
  	let active = '';
  import { onMount } from 'svelte';
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
	
  
  export const equipment = [
		
   
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
</script>


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