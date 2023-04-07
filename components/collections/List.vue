<template>
  <div>
    <div v-if="!applications.length">
      <p class="h3">No Application found, Please add an application to continue</p>
    </div>
    <table  class="border bg-opacity-75 container px-4 sm:px-6">
      <div v-for="(application, index) in props.applications" :key="index">
        <div>
          <tbody>
            <tr>
              <td>
                ID - {{ application.candidate_id }}
              </td>
            </tr>
            <tr>
              <td>
                JOB-ID - {{ application.job_posting_id }}
              </td>

            </tr>
            <tr>
              <td>
                STATUS - {{ application.status }}
              </td>
            </tr>
            <tr>
              <td>
                RESUME URL - {{ application.resume_url }}
              </td>
            </tr>
            <tr>
              <td>
                COVER LETTER URL - {{ application.cover_letter }}
              </td>
            </tr>

          </tbody>

        </div>
        <hr v-if="applications.length > 1" class="border space-y-8 mt-5" />
      </div>
    </table>
  </div>
</template>
<script setup>
import { Menu, MenuButton, MenuItem, MenuItems, Dialog, DialogPanel, DialogTitle, TransitionChild, TransitionRoot } from "@headlessui/vue";
import { CodeBracketIcon, EllipsisVerticalIcon, FlagIcon, StarIcon } from "@heroicons/vue/20/solid";
import { PencilIcon } from "@heroicons/vue/24/outline";

// Define props
const props = defineProps({
  applications: Array,
});

// Define emit events
const emit = defineEmits(["edit", "delete"]);
</script>
