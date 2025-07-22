<script setup>
import InputLabel from '@/Components/InputLabel.vue';
import TextInput from '@/Components/TextInput.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head,useForm } from '@inertiajs/vue3';

const form = useForm({
       title: "",
       body: ""
})

function submit(){
       form.post(route('posts.store'), {
              preserveScroll: true,
              onSuccess: () => form.reset()
       })
}

</script>

<template>
    <Head title="Create Posts" />

    <AuthenticatedLayout>
        <template #header>
            <h2
                class="text-xl font-semibold leading-tight text-gray-800"
            >
                Create Posts
            </h2>
        </template>
              <GuestLayout>
                     <div >
                            <form @submit.prevent="submit" >
                                   <div>
                                          <InputLabel for="title" value="Title" />
                            
                                          <TextInput
                                                 id="title"
                                                 type="title"
                                                 class="mt-1 w-1/2 flex justify-center"
                                                 v-model="form.title"
                                                 required
                                          />
                            
                                          <InputError class="mt-2" :message="form.errors.title" />
                                   </div>

                                   <div class="mt-4">
                                          <InputLabel for="body" value="Body" />
                            
                                          <textarea
                                                 id="body"
                                                 type="body"
                                                 class="mt-1 w-1/2 flex justify-center"
                                                 v-model="form.body"
                                                 required
                                          ></textarea>
                            
                                          <InputError class="mt-2" :message="form.errors.body" />
                                   </div>
                                   <div class="mt-4">
                                          <PrimaryButton
                                                 class="ms-4"
                                                 :class="{ 'opacity-25': form.processing }"
                                                 :disabled="form.processing"
                                                 >
                                                 Save
                                          </PrimaryButton>
                                   </div>
                            </form>
                     </div>
              </GuestLayout>
    </AuthenticatedLayout>
</template>
