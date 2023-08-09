<script setup>
import { ref, defineProps, computed } from 'vue';
import { useStore } from 'vuex';
import { faBars, faTimes,faSignOut,faDashboard,faInbox,faClipboard,faLayerGroup,faUserGear,faMoneyCheck } from '@fortawesome/free-solid-svg-icons';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
import { Head, Link, router } from '@inertiajs/vue3';
import Dropdown from '@/Components/Dropdown.vue';
import DropdownLink from '@/Components/DropdownLink.vue';
import NavLinkSidebar from '@/Components/NavLinkSidebar.vue';
const props = defineProps({
  isSidebarCollapsed: Boolean
});

const store = useStore();
const isSidebarCollapsed = computed(() => store.state.isSidebarCollapsed);
const toggleSidebar = () => store.commit('toggleSidebar');

const icons = {
  bars: faBars,
  times: faTimes,
  signout: faSignOut,
  dashboard: faDashboard,
  inbox:faInbox,
  clipboard:faClipboard,
  layergroup:faLayerGroup,
  usergear:faUserGear,
  money:faMoneyCheck
};
</script>

<template>
  <div class="">
    <!-- Sidebar -->
    <aside
      :class="{'hidden': isSidebarCollapsed, 'h-screen': !isSidebarCollapsed}"
      class="bg-white shadow border right-3 ring-offset-2 border-slate-600"
    >
      <!-- Sidebar Logo -->
      <div class="p-4 bg-gray-100 text-center">
        <img src="/public/" alt="Logo" class="w-16 h-16 mx-auto">
        <h1 class="text-xl font-semibold mt-2">Sistem Informasi</h1>
      </div>

      <!-- Sidebar Items -->
      <ul class="mt-4 space-y-2">
        <li>
            
           <NavLinkSidebar :href="route('dashboard')" :active="route().current('dashboard')">
            <span class="h-6 w-8 text-slate-400"><font-awesome-icon :icon="icons.dashboard"/></span>
                Dashboard
           </NavLinkSidebar>
         
    
        </li>
        <li>
            
            <NavLinkSidebar :href="route('pengajuan.index')" :active="route().current('pengajuan.index')">
             <span class="h-6 w-8 text-slate-400"><font-awesome-icon :icon="icons.inbox"/></span>
                 Data Pengajuan
            </NavLinkSidebar>
          
     
         </li>

         <li>
            
            <NavLinkSidebar :href="route('pengajuan.index')" :active="route().current('pengajuan.index')">
             <span class="h-6 w-8 text-slate-400"><font-awesome-icon :icon="icons.clipboard"/></span>
                 Data Revisi
            </NavLinkSidebar>
          
     
         </li>
         <li>
            
            <NavLinkSidebar :href="route('pengajuan.index')" :active="route().current('pengajuan.index')">
             <span class="h-6 w-8 text-slate-400"><font-awesome-icon :icon="icons.layergroup"/></span>
                 Rekapitulasi
            </NavLinkSidebar>
          
     
         </li>
         <li>
            
            <NavLinkSidebar :href="route('pengajuan.index')" :active="route().current('pengajuan.index')">
             <span class="h-6 w-8 text-slate-400"><font-awesome-icon :icon="icons.usergear"/></span>
                 User Management
            </NavLinkSidebar>
         </li>
         <li>
            
            <NavLinkSidebar :href="route('pengajuan.index')" :active="route().current('pengajuan.index')">
             <span class="h-6 w-8 text-slate-400"><font-awesome-icon :icon="icons.money"/></span>
                 Data Claim
            </NavLinkSidebar>
         </li>
         <li>
            
            <NavLinkSidebar :href="route('pengajuan.index')" :active="route().current('pengajuan.index')">
             <span class="h-6 w-8 text-slate-400"><font-awesome-icon :icon="icons.money"/></span>
                 Pengaturan Aplikasi
            </NavLinkSidebar>
         </li>
         <li>
            <Dropdown align="bottom" width="full">
                <template #trigger>

                    <a href="#" class="flex items-center p-3 space-x-2 hover:bg-gray-100">
                        <svg
                          xmlns="http://www.w3.org/2000/svg"
                          class="h-6 w-6 text-slate-600"
                          fill="none"
                          viewBox="0 0 24 24"
                          stroke="currentColor"
                        >
                          <!-- Masukkan kode SVG ikon yang sesuai di sini -->
                        </svg>
                        <span>Pengajuan</span>
                        <span class=" absolute top-1/2 -translate-y-1/2 transform transition-transform duration-300">
                            <svg
                              xmlns="http://www.w3.org/2000/svg"
                              class="h-4 w-4 text-slate-600"
                              fill="none"
                              viewBox="0 0 24 24"
                              stroke="currentColor"
                            >
                              <path
                                stroke-linecap="round"
                                stroke-linejoin="round"
                                d="M19.5 8.25l-7.5 7.5-7.5-7.5"
                              />
                            </svg>
                          </span>

                    </a>
                
                </template>
        
                <template #content>
                  <li class="block px-4 py-2 text-xs text-gray-400">Manage Account</li>
        
                  <li>
                    <DropdownLink :href="route('profile.show')">Profile</DropdownLink>
                  </li>
        
                  <li v-if="$page.props.jetstream.hasApiFeatures">
                    <DropdownLink :href="route('api-tokens.index')">API Tokens</DropdownLink>
                  </li>
        
                  <li class="border-t border-gray-200" />
        
                  <li>
                    <form @submit.prevent="logout">
                      <DropdownLink as="button">Log Out</DropdownLink>
                    </form>
                  </li>
                </template>
              </Dropdown>
          </li>
        
       
      </ul>
    </aside>

    <!-- Rest of the page content -->
    <slot></slot>
  </div>
</template>
