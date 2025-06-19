<script>
 
  
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

<section class="bg-primary-500 py-16 px-4 md:px-16 w-full" id="top">
  <div class="max-w-7xl mx-auto">
      <h2 class="text-3xl font-semibold mb-6">We Specialize In</h2>

      <div class="md:hidden overflow-x-auto py-2 -mx-2 px-2">
          <div class="flex gap-4 w-max">
              {#each equipment as item}
                  <div class="p-6 border text-primary-500 border-mediumBlue/20 rounded-xl shadow-2xl shadow-neutral-950 bg-primary-900 hover:shadow-md transition min-w-[280px]">
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

      <div class="hidden md:grid md:grid-cols-3 gap-6">
          {#each equipment as item}
              <div class="p-6 border text-primary-500 border-mediumBlue/20 rounded-xl shadow-2xl shadow-neutral-950 bg-primary-900 hover:shadow-md transition">
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