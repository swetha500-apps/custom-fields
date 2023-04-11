<template>
   <nav class="container mx-auto p-4 ">
              <div class="flex justify-evenly">
                <div><NuxtLink to="/testcollection" class="font-bold"><div class="flex ml-2"><div></div><div></div></div></NuxtLink></div>
              
            </div></nav>
          <div>
            <slot />
          </div>
</template>
<script setup lang="ts">
import {ClipboardDocumentIcon,BuildingOfficeIcon,IdentificationIcon,HomeModernIcon,BuildingStorefrontIcon} from '@heroicons/vue/24/outline'
</script>