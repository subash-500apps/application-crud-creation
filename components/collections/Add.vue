<template>
  <div>
    <div>
      <div class="mt-2">
        <input
          placeholder=" Candidate ID"
          v-model="candidate_id"
          type="text"
          name="email"
          id="email"
          class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        />
      </div>
      <div class="mt-2">
        <input
          placeholder=" JOB POSTING ID"
          v-model="job_posting_id"
          type="text"
          name="email"
          id="email"
          class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        />
      </div>
      <div class="mt-2">
        <input
          placeholder=" STATUS"
          v-model="status"
          type="text"
          name="email"
          id="email"
          class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        />
      </div>

      <div class="mt-2">
        <input
          placeholder=" RESUME URL"
          v-model="resume_url"
          type="text"
          name="email"
          id="email"
          class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        />
      </div>
      <div class="mt-2">
        <input
          placeholder=" COVER LETTER"
          v-model="cover_letter"
          type="text"
          name="email"
          id="email"
          class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        />
      </div>
    </div>
    <div class="mt-5 sm:mt-6 sm:grid sm:grid-flow-row-dense sm:grid-cols-2 sm:gap-3">
      <button
        type="button"
        class="inline-flex w-full justify-center rounded-md bg-gray-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 sm:col-start-2"
        @click="saveTask(false)"
      >
        Save
      </button>

      <button type="button" class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:col-start-1 sm:mt-0" @click="closeModal(false)">
        Cancel
      </button>
    </div>
  </div>
</template>
<script setup>
  const job_posting_id = ref("");
  const candidate_id = ref("");
  const status = ref("");
  const resume_url = ref("");
  const cover_letter = ref("");
  const emit = defineEmits(["save-task", "hide"]);
  const url = "https://v7-stark-db-orm.mercury.infinity-api.net/api/applications/";
  // Close modal
  const closeModal = (close) => {
    emit("hide", close);
  };
  // Save task
  const saveTask = async (close) => {
    console.log("after save", job_posting_id.value, candidate_id.value, status.value, resume_url.value);
    emit("hide", close);
    //emit("Addtask", form);
    const { data } = await useAuthLazyFetchPost(`${url}`, {
      body: {
        candidate_id: candidate_id.value ? candidate_id.value : "",
        job_posting_id: job_posting_id.value ? job_posting_id.value : "",
        status: status.value ? status.value : "",
        resume_url: resume_url.value ? resume_url.value : "",
        cover_letter: cover_letter.value ? cover_letter.value : "",
        track_info: [],
        questionnaire: [],
      },
    });
    emit("Addtask", data);
    console.log("data post", data.value);
  };
</script>
