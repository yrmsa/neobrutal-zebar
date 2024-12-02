<script lang="ts">
  type ButtonProps = {
    iconClass: string;
    label?: string;
    callback?: () => void;
    class: string;
    index?: number;
  };
  let { iconClass, label, callback, index, ...rest }: ButtonProps = $props();
</script>

<button
  class="flex bg-blend-30 border border-zb-border rounded-base shadow-button hover:translate-x-boxShadowX hover:translate-y-boxShadowY hover:shadow-none p-1 {rest.class}"
  onclick={callback}
  aria-label={label}
>
  {#if index != undefined}
    <span class="text-xs">{index}</span>
  {/if}
  <i class="ti ti-{iconClass}"></i>
</button>
