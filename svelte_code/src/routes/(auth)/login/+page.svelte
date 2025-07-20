<script lang="ts">
  import { superForm } from "sveltekit-superforms";
  import { formSchema } from "./form_schema";
  import { zodClient } from "sveltekit-superforms/adapters";
  import FormError from "$lib/components/FormError.svelte";
  import { toast } from "svelte-sonner";
  import login_land from "$lib/static/login_land.png";

  export let data;

  const { form, errors, enhance } = superForm(data.form, {
    validators: zodClient(formSchema),
    onError: (e) => {
      console.error(e);
      // TODO: make red
      toast.error(`Something went wrong at server`);
    },
  });
</script>

<div
  class="min-h-screen flex items-center justify-center w-screen"
>
  <form
    method="POST"
    action="?/login"
    use:enhance
    class="card glass p-10 flex flex-col  w-auto gap-3"
  >
    <h1 class="text-center text-3xl mb-3 mt-4">Welcome Back!</h1>
    <img
      src={login_land}
      alt="Login illustration"
      class="mx-auto w-auto sm:w-36 h-auto sm:h-36"
    />
    <div class="flex flex-col mx-auto p-3 justify-center w-full">
      <label>
        <span class="label-text">Email</span>
        <input
          class="input input-bordered"
          type="email"
          placeholder="Your email"
          name="email"
          bind:value={$form.email}
        />
        <FormError errors={$errors.email} />
      </label>

      <label>
        <span class="label-text">Password</span>
        <input
          class="input input-bordered"
          type="password"
          placeholder="********"
          name="password"
          bind:value={$form.password}
        />
        <FormError errors={$errors.password} />
      </label>

      <button type="submit" class="mt-2 btn bg-[#D3DAD9] hover:bg-[#A8C3BC] mx-auto w-[60%] ">Sign In</button>
    </div>

    <div class="flex justify-around">
      <a class="btn btn-ghost btn-sm" href="/register">Register </a>
      <a class="btn btn-ghost btn-sm" href="/forgotPassword">Forgot Password?</a>
    </div>
  </form>
</div>
