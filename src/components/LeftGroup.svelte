<script lang="ts">
  import type { BatteryOutput, CpuOutput, MemoryOutput } from "zebar";

  import Button from "./Button.svelte";
  import Meter from "./Meter.svelte";

  type LeftGroupProps = {
    battery: BatteryOutput;
    cpu: CpuOutput;
    memory: MemoryOutput;
  };

  let { battery, cpu, memory }: LeftGroupProps = $props();
</script>

<div class="flex flex-row gap-3 items-center">
  <Button class="text-zb-icon" iconClass="heartbeat" />
  <div class="flex gap-1 items-center">
    <i class="ti ti-ruler-2"></i>
    <Meter class="bg-zb-memory" percent={Math.round(memory?.usage ?? 0)} />
  </div>
  <div class="flex gap-1 items-center">
    <i class="ti ti-cpu"></i>
    <Meter class="bg-zb-cpu" percent={Math.round(cpu?.usage ?? 0)} />
  </div>
  <div class="flex gap-1 items-center">
    {#if battery?.isCharging}
      <i class="ti ti-battery-vertical-charging"></i>
    {/if}
    {#if !battery?.isCharging}
      {#if Math.round(battery?.chargePercent) >= 80}
        <i class="ti ti-battery-vertical-4"></i>
      {:else if Math.round(battery?.chargePercent) >= 60}
        <i class="ti ti-battery-vertical-3"></i>
      {:else if Math.round(battery?.chargePercent) >= 40}
        <i class="ti ti-battery-vertical-2"></i>
      {:else if Math.round(battery?.chargePercent) >= 20}
        <i class="ti ti-battery-vertical-1"></i>
      {:else}
        <i class="ti ti-battery-vertical-exclamation"></i>
      {/if}
    {/if}
    <Meter
      class="bg-zb-battery-good"
      percent={Math.round(battery?.chargePercent ?? 100)}
    />
  </div>
</div>
