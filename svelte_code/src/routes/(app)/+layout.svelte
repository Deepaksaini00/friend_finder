<script lang="ts">
  import { page } from "$app/stores";
  import { CircleUserRound, LogOut, Send } from "lucide-svelte";
  import type { ChangeEvent } from "sveltekit-superforms";
  import { MapPin, User } from "lucide-svelte";

  type users = {
    username: string;
    pincode: number;
    avatar: string;
  };
  let val = "";
  let timer: number | undefined;
  let showActive = false;
  export let inputval = "";
  let users: users[] = [];

  const debounce = (event: any) => {
    const text = event.target.value;
    clearTimeout(timer);
    timer = setTimeout(() => {
      val = text;
      if (inputval.length > 1) {
        finder();
      } else {
        users = [];
      }
    }, 750);
  };

  export async function finder() {
    const response = await fetch(
      `/roll/?inputval=${encodeURIComponent(inputval)}`,
    );
    const data = await response.json();
    users = data.users;
  }
</script>

<nav class="navbar shadow fixed top-0 z-10 bg-[#6CA296]">
  <div class="flex-1">
    <a href="/" class="btn btn-ghost text-xl">Friend Finder</a>
  </div>

  <div class="relative flex items-center gap-5 mr-8">
    <div class="relative form-control">
      <input
        type="text"
        placeholder="Search"
        class="input input-bordered w-64"
        bind:value={inputval}
        on:focus={() => (showActive = true)}
        on:blur={() => (showActive = false)}
        on:input={(event) => debounce(event)}
      />

      <div class="absolute flex flex-col pt-1 mt-10 w-full z-50">
        <ul
          class="flex flex-col justify-center bg-gray-300 w-full divide-y divide-gray-400"
        >
          {#if users.length > 0 && showActive}
            {#each users as user}
              <li class="p-2 hover:bg-gray-400 flex itmes-center gap-x-4">
                <a
                  href={`/user/${user.username}`}
                  class="flex items-center gap-x-4 w-full"
                >
                  <img
                    src={`/avatar/${user.avatar}`}
                    alt="?"
                    class="h-12 w-12 rounded-full"
                  />
                  <div class="flex flex-col">
                    <h5 class="font-semibold">{user.username}</h5>

                    <span class="text-sm">{user.pincode}</span>
                  </div>
                </a>
              </li>
            {/each}
          {:else if showActive}
            <h3 class="text-sm mt-4">No User Found!</h3>
          {/if}
        </ul>
      </div>
    </div>

    <div class="flex-none gap-5 mr-8">
      <a href="/chat" class="btn btn-ghost btn-circle">
        <div class="indicator">
          <Send />
        </div>
      </a>
      <div class="dropdown dropdown-end">
        <div tabindex="0" role="button" class="btn btn-ghost btn-circle avatar">
          <CircleUserRound />
        </div>
        <ul
          tabindex="0"
          role="listbox"
          class="flex flex-col gap-2 dropdown-content bg-base-100 rounded-box z-[1] mt-3 w-52 p-4 shadow items-stretch"
        >
          <li>
            <a href="/profile" class="btn btn-sm w-full btn-ghost"> Profile </a>
          </li>
          <li>
            <form method="POST" action="/login?/logout" class="w-full">
              <button class="btn btn-sm w-full btn-ghost" type="submit"
                >Logout</button
              >
            </form>
          </li>
        </ul>
      </div>
    </div>
  </div>
</nav>
{#if showActive}
  <div class="fixed inset-0 z-0 backdrop-blur-sm bg-white/10"></div>
{/if}

<div class="pt-20 m-auto max-w-screen-lg md:px-5 px-2">
  <slot></slot>
</div>

{#if $page.url.pathname === "/"}
  <footer
    class="footer footer-center bg-[#CCCCCC] text-base-content fixed h-10 bottom-0 left-0 w-full"
  >
    <aside>
      <p>
        Copyright © {new Date().getFullYear()} - All right reserved by Deepak saini
      </p>
    </aside>
  </footer>
{/if}
