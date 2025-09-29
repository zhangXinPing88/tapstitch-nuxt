<script setup lang="ts">
import { postsQuery, settingsQuery } from "~/sanity/queries";
import type { PostsQueryResult, SettingsQueryResult } from "~/sanity/types";

const { data: posts } = await useSanityQuery<PostsQueryResult>(postsQuery);
const { data: settings } =
  await useSanityQuery<SettingsQueryResult>(settingsQuery);

useSiteMetadata({
  title: "Sanity + Nuxt",
  description:
    "This starter template is a powerful web app built with Nuxt for the frontend and Sanity for seamless content management. It includes a standalone Sanity Studio (CMS) with advanced features like Visual Editing, type-safe schemas and queries using Sanity TypeGen , a structured content page builder, and more. The @nuxtjs/sanity toolkit is integrated into the frontend, ensuring a quick and effortless setup.",
  ogImage: settings?.value?.ogImage || "",
});

usePageAnimation();
</script>

<template>
  <div v-if="posts" class="border-t border-gray-100">
    <div class="container">
      <aside class="py-12 sm:py-20">
        <Posts
          heading="Recent Posts"
          :subHeading="`These ${posts.length} blog posts are populated from your Sanity Studio.`"
          :posts="posts"
        />
      </aside>
    </div>
  </div>
</template>
