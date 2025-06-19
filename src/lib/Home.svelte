<script>

let active = '';
let currentIndex = 0;
	let direction = '';
	let animClass = '';

    
	const images = ['./front.jpg', './front2.png', './front3.png'];

function clearAnimation() {
    setTimeout(() => {
        direction = '';
        animClass = '';
    }, 500);
}

function prevSlide() {
    direction = 'left';
    animClass = 'slide-left';
    currentIndex = (currentIndex - 1 + images.length) % images.length;
    clearAnimation();
}

function nextSlide() {
    direction = 'right';
    animClass = 'slide-right';
    currentIndex = (currentIndex + 1) % images.length;
    clearAnimation();
}

const autoSlide = setInterval(() => {
    nextSlide();
}, 7000);

</script>

<div class="relative w-full overflow-hidden h-[300px] sm:h-[600px]">
	
    <img
        src={images[currentIndex]}
        alt="slide"
        class="absolute w-full h-full object-cover z-0 {animClass}"
    />

    <!-- Overlay with tagline + Contact Us -->
    <div class="absolute inset-0 bg-primary-900/60 flex items-center z-10">
        <div class="mx-auto text-center text-primary-500">
            <div class="text-3xl sm:text-5xl md:text-7xl font-extralight brightness-200">"Engineering Progress"</div>
            <div class="text-2xl sm:text-3xl  text-primary-300 font-bold md:text-5xl mt-2">"Designing the Future"</div>

            <!-- Contact Us Link -->
            <a
                href="#contact"
                on:click={() => (active = 'contact')}
                class:bg-primary-300={active === 'contact'}
                class:px-6={active === 'contact'}
                class="my-10 animate-bounce relative inline-flex items-center justify-center p-4 px-6 py-3 overflow-hidden font-medium text-primary-300 transition duration-300 ease-out border-2 border-primary-300 rounded-full shadow-md group"
            >
                <span
                    class="absolute inset-0 flex items-center justify-center w-full h-full text-primary-500 duration-300 -translate-x-full bg-primary-300 group-hover:translate-x-0 ease"
                >
                    <svg
                        class="w-6 h-6"
                        fill="none"
                        stroke="currentColor"
                        viewBox="0 0 24 24"
                        xmlns="http://www.w3.org/2000/svg"
                        ><path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            d="M14 5l7 7m0 0l-7 7m7-7H3"
                        ></path></svg
                    >
                </span>
                <span
                    class="absolute flex items-center justify-center w-full h-full text-primary-500 transition-all duration-300 transform group-hover:translate-x-full ease"
                    >Contact Us</span
                >
                <span class="relative invisible">Button Text</span>
            </a>
        </div>
    </div>

    <!-- Arrows -->
    <button
        on:click={prevSlide}
        class="absolute left-4 cursor-pointer hidden sm:block top-1/2 -translate-y-1/2 z-20 bg-black/40 text-white px-4 py-2 text-2xl rounded-full hover:bg-black/70"
        >‹</button
    >
    <button
        on:click={nextSlide}
        class="absolute right-4 hidden cursor-pointer sm:block top-1/2 -translate-y-1/2 z-20 bg-black/40 text-white px-4 py-2 text-2xl rounded-full hover:bg-black/70"
        >›</button
    >
</div>