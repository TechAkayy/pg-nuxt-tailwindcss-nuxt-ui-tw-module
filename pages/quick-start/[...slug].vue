<script setup lang="ts">
  const slug = useRoute().params.slug.toString().replace(/,/g, '/')
  const { data: post } = await useAsyncData(slug, () => {
    return queryContent(slug).findOne()
  })

  definePageMeta({
    name: 'quick-start',
    navOrder: 2,
  })

  useHead({
    title: post.value.title,
  })
</script>
<template>
  <div class="pb-12">
    <TheHeader>
      <div>
        <div class="flex items-center">
          <h2 class="text-5xl">Quick Start</h2>
        </div>
        <div class="flex items-center mt-2">
          <h6 class="mt-2">Github repo for this template</h6>
          <NuxtLink
            href="https://github.com/pinegrow/pg-nuxt-tailwindcss"
            target="_blank"
            external
          >
            <BaseButton
              size="x-small"
              class="ml-2"
              variant="outlined"
              container
              tag="span"
              role="primary"
            >
              <span>Click here</span>
            </BaseButton>
          </NuxtLink>
        </div>
        <slot />
      </div>
    </TheHeader>
    <section>
      <BaseSheet class="container mx-auto px-10 w-full">
        <div class="flex flex-col rounded-lg" container>
          <article
            class="dark:xl:divide-gray-700 xl:divide-gray-200 xl:divide-y"
          >
            <div
              class="dark:divide-gray-700 divide-gray-200 divide-y pb-16 xl:divide-y-0 xl:gap-x-10 xl:grid xl:grid-cols-4 xl:pb-20 xl:sticky"
              style="grid-template-rows: auto 1fr"
            >
              <div
                class="dark:divide-gray-700 divide-gray-200 divide-y xl:col-span-3 xl:pb-0 xl:row-span-2"
              >
                <div
                  id="post"
                  class="dark:prose-invert dark:prose-neutral-100 flex flex-col heading-offset max-w-none prose prose-neutral-800 rounded-lg"
                >
                  <ContentRenderer id="content" :value="post">
                    <template #empty>
                      <p>No content found.</p>
                    </template>
                  </ContentRenderer>
                </div>
              </div>
            </div>
          </article>
        </div>
      </BaseSheet>
    </section>
  </div>
</template>
<style scoped></style>
