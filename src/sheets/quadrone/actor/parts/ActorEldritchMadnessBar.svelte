<script lang="ts">
  interface Props {
    level: number;
    total: number;
    onEldritchMadnessLevelSet?: (level: number) => void;
    onClose?: () => void;
  }

  let { level, total, onEldritchMadnessLevelSet, onClose }: Props = $props();

  let effectiveTotal = $derived(total + 1);
</script>

<div class="eldritch-madness-bar flexrow">
  {#each Array(effectiveTotal) as _, i}
    <button
      aria-label="Eldritch Madness Level {i}"
      type="button"
      class={[
        'button button-borderless button-icon-only button-config',
        { active: i === level },
      ]}
      onclick={() => {
        onEldritchMadnessLevelSet?.(i);
        onClose?.();
      }}
      data-tooltip
    >
      {i}
    </button>
  {/each}
  <button
    aria-label="Close eldritch madness bar"
    type="button"
    class="button button-borderless button-icon-only button-config"
    onclick={() => onClose?.()}
  >
    <i class="fas fa-times"></i>
  </button>
</div>
