<script setup lang="ts">
const routes = useRouter().getRoutes().sort((a,b)=>a.name > b.name? 1:-1)

</script>

<template>
<div class="drawer">
  <input id="my-drawer-3" type="checkbox" class="drawer-toggle" /> 
  <div class="drawer-content flex flex-col">
    <!-- Navbar -->
    <div class="w-full navbar bg-base-300">
      <div class="flex-none lg:hidden">
        <label for="my-drawer-3" aria-label="open sidebar" class="btn btn-square btn-ghost">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" class="inline-block w-6 h-6 stroke-current"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path></svg>
        </label>
      </div> 
      <div class="flex-1 px-2 mx-2 font-bold text-2xl">vee-validate基礎</div>
      <div class="flex-none hidden lg:block">
        <ul class="menu menu-horizontal">
          <!-- Navbar menu content here -->
          <li v-for="r of routes"><a  @click="navigateTo(r.path)">{{ r.name }}</a></li>
        </ul>
      </div>
    </div>
    <!-- Page content here -->
    
    <NuxtPage />
  </div>

  <div class="drawer-side">
    <label for="my-drawer-3" aria-label="close sidebar" class="drawer-overlay"></label> 
    <ul class="menu p-4 w-80 min-h-full bg-base-200">
      <!-- Sidebar content here -->
      <li><a v-for="r of routes" @click="navigateTo(r.path)">{{ r.name }}</a></li>
    </ul>
  </div>
</div>

</template>
