<template>
  <div class="p-4">
    <!-- List Applications -->
    <div>
      <div class="space-y-8">
        <div>
          <p class="h3">APPLICATION DETAILS</p>
        </div>
        <button @click="openModel" type="button"
          class="rounded-md bg-gray-600 px-3.5 py-2.5 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">
          CREATE APPLICATION
        </button>
      </div>
      <div class="py-6">
        <Collections-List :applications="applications"></Collections-List>
      </div>
      <!--Add Application modal-->
      <TransitionRoot as="template" :show="open">
        <Dialog as="div" class="relative z-10" @close="open = false">
          <TransitionChild as="template" enter="ease-out duration-300" enter-from="opacity-0" enter-to="opacity-100"
            leave="ease-in duration-200" leave-from="opacity-100" leave-to="opacity-0">
            <div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity" />
          </TransitionChild>

          <div class="fixed inset-0 z-10 overflow-y-auto">
            <div class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0">
              <TransitionChild as="template" enter="ease-out duration-300"
                enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
                enter-to="opacity-100 translate-y-0 sm:scale-100" leave="ease-in duration-200"
                leave-from="opacity-100 translate-y-0 sm:scale-100"
                leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95">
                <DialogPanel
                  class="relative transform overflow-hidden rounded-lg bg-white px-4 pb-4 pt-5 text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg sm:p-6">
                  <CollectionsAdd @hide="closeModel" @addApplication="saveApplication"></CollectionsAdd>
                </DialogPanel>
              </TransitionChild>
            </div>
          </div>
        </Dialog>
      </TransitionRoot>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { Menu, MenuButton, MenuItem, MenuItems, Dialog, DialogPanel, DialogTitle, TransitionChild, TransitionRoot } from "@headlessui/vue";
import { CodeBracketIcon, EllipsisVerticalIcon, FlagIcon, StarIcon } from "@heroicons/vue/20/solid";
const open = ref(false);
const applications = ref([])

// Open modal
const openModel = () => {
  open.value = true;
};
// Close modal
const closeModel = (e: any) => {
  open.value = false;
  open.value = e;
};
// Save Application
const saveApplication = (newapplication: any) => {
  if (newapplication) {
    applications.value.unshift(newapplication.value)
  }
}
</script>
