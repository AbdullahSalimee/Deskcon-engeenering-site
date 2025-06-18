<script>
	import { onMount } from 'svelte';
 export let active = '';

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

<nav class="flex w-full p-2 h-20 bg-primary-900 sticky top-0 z-50">
    <!-- svelte-ignore a11y_invalid_attribute -->
    <a
        href="/"
        on:click={(e) => {
            e.preventDefault();
            active = '';
            window.scrollTo({ top: 0, behavior: 'smooth' });
            history.pushState(null, '', '/'); // This clears the hash from URL
        }}
        class="flex-none justify-center place-content-center mx-12"
    >
        <img src="./logo.png" alt="" class="w-24" />
    </a>

    <div class="flex grow items-center w-full h-full">
        <a
            href="#team"
            on:click={() => (active = 'team')}
            class="hover:bg-primary-300 hover:px-6 px-3 text-primary-500 font-heading place-content-center h-full border-primary-300 border-l-2 border-r duration-300 ease-in-out"
            class:bg-primary-300={active === 'team'}
            class:px-6={active === 'team'}
        >
            Our Team
        </a>
        <a
            href="#projects"
            on:click={() => (active = 'projects')}
            class=" px-3 text-primary-500 hover:bg-primary-300 hover:px-6 font-heading place-content-center h-full border-primary-300 border-l border-r duration-300 ease-in-out"
            class:bg-primary-300={active === 'projects'}
            class:px-6={active === 'projects'}
        >
            Projects
        </a>
        <a
            href="#services"
            on:click={() => (active = 'services')}
            class=" px-3 text-primary-500 font-heading hover:bg-primary-300 hover:px-6 place-content-center h-full border-primary-300 border-l border-r duration-300 ease-in-out"
            class:bg-primary-300={active === 'services'}
            class:px-6={active === 'services'}
        >
            Services
        </a>
        <a
            href="#vision"
            on:click={() => (active = 'vision')}
            class=" px-3 text-primary-500 font-heading place-content-center h-full hover:bg-primary-300 hover:px-6 border-primary-300 border-l border-r duration-300 ease-in-out"
            class:bg-primary-300={active === 'vision'}
            class:px-6={active === 'vision'}
        >
            V & M
        </a>
        <a
            href="#about"
            on:click={() => (active = 'about')}
            class=" px-3 text-primary-500 font-heading hover:bg-primary-300 hover:px-6 place-content-center h-full border-primary-300 border-l border-r-2 duration-300 ease-in-out"
            class:bg-primary-300={active === 'about'}
            class:px-6={active === 'about'}
        >
            About Us
        </a>
        <a
            href="#contact"
            on:click={() => (active = 'contact')}
            class=" ml-auto px-3 text-primary-500 font-heading place-content-center hover:bg-primary-300 hover:px-6 h-full border-primary-300 border-l-2 border-r-2 duration-300 ease-in-out"
            class:bg-primary-300={active === 'contact'}
            class:px-6={active === 'contact'}
        >
            contact
        </a>
    </div>
</nav>