<script>
	import { onMount } from "svelte";

	
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

</script>


<section id="team" class="bg-primary-900 py-16 md:py-24 px-4 md:px-16 relative">
    <div class="md:w-1/2 lg:1/3 mx-auto">
        <h2 class="text-4xl font-bold my-12 text-primary-300 text-center">Our Team</h2>

        <div class="relative overflow-hidden p-6">
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