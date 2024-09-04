<script lang="ts">
  import type { DefaultDataPoint } from 'chart.js-v4';
  import { Chart as ChartJS, PieController } from 'chart.js-v4';
  import type { ChartBaseProps } from './types/index.js';
  import Chart from './Chart.svelte';
  import { useForwardEvents } from './utils/index.js';

  interface $$Props<TData = DefaultDataPoint<'pie'>, TLabel = unknown>
    extends Omit<ChartBaseProps<'pie', TData, TLabel>, 'type'> {
    chart?: ChartJS<'pie', TData, TLabel> | null;
  }

  ChartJS.register(PieController);

  export let chart: $$Props['chart'] = null;
  let props: $$Props;
  let baseChartRef: Chart;

  useForwardEvents(() => baseChartRef);

  $: props = $$props as $$Props;
</script>

<Chart bind:this={baseChartRef} bind:chart type="pie" {...props} />
