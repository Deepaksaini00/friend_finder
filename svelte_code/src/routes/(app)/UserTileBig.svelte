<script lang="ts">
  import { formatDistance } from "date-fns";
  import type { Components } from "../../backend_openapi";
  import { Mail, MapPin, Star, User } from "lucide-svelte";

  export let user_info: Components.Schemas.UserWithTopics;

  export let show_email: boolean = false;
  export let show_name:boolean=false;

</script>

<div class="flex h-64 w-full items-center mt-6">
  <div class="h-full aspect-square">
    <img
      src = {`/avatar/${user_info.user.avatar}`}
      class="h-full w-full p-8 rounded-full "
      alt="profile"
    />
  </div>
  <div class="grow flex flex-col m-3">
    <div class="basis-0 grow flex gap-2 flex-col">
      <div class="flex flex-col gap-2">
        <h3 class="text-4xl font-bold hover:underline">
          @{user_info.user.username}
        </h3>
        {#if show_name}
          <h3 class="text-2xl font-bold ">{user_info.user.name}</h3>
        {/if}
      </div>

      <div class="flex flex-col gap-2">
        <p class="text-md">
          Joined {formatDistance(user_info.user.joined_on, new Date())} ago
        </p>
        <p class="text-lg flex gap-2 items-center">
          <MapPin size={20} />
          {user_info.user.pincode}
        </p>
        <p class="text-lg flex gap-2 items-center">
          <Star size={20} />
          {user_info.topics.map((x) => x.name).join(" | ")}
        </p>
        {#if show_email}
          <p class="text-lg flex gap-2 items-center">
            <Mail size={20} />
            {user_info.user.email}
          </p>
        {/if}
      </div>
    </div>
  </div>
</div>
