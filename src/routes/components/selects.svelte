<script>
  import { Select } from "smelte";
  import { Button } from "smelte";
  import Code from "docs/Code.svelte";
  import { Checkbox } from "smelte";
  import { Card} from "smelte";
  import selects from "examples/selects.txt";

  let value1 = "";
  let value2 = "";
  let value3 = "";
  let value4 = "";

  let showList = false;

  let items = [
    { value: 1, text: "Select Item 1" },
    { value: 2, text: "Select Item 2" },
    { value: 3, text: "Select Item 3" },
    { value: 4, text: "Select Item 4" },
  ];
  $: itemsLabel = items.map(i => i.text).join(", ");

  let selectedItems = [];

  function toggle(i) {
    return v => v.detail
      ? selectedItems.push(i)
      : selectedItems = selectedItems.filter(si => si !== i);
  }

  $: selectedLabel = selectedItems.map(i => i.text).join(", ");

  const label = "A select";
</script>

<p>
  One may bind to a select via
  <span class="code-inline">on:change</span>
  event.
</p>
<caption>Selected: {value1 || 'nothing'}</caption>
<Select {label} {items} on:change={v => (value1 = v.detail)} />

<p>
Updates when the underlying items change
</p>
<caption>Items: {itemsLabel || 'nothing'}</caption>
<div>
  <Button on:click="{e => {items = [...items, { value: (items.length + 1), text: 'Select Item ' + (items.length + 1)}]}}">Add item</Button>
</div>


<Code code={selects} />

<p>
  Or through binding
  <span class="code-inline">on:value</span>
  .
</p>
<caption>Selected: {value2 || 'nothing'}</caption>
<Select color="success" bind:value={value2} {label} {items} />

<p>Select may be outlined.</p>
<Select bind:value={value2} outlined {label} {items} />

<p>Select may even be an autocomplete search component.</p>
<caption>Selected: {value3 || 'nothing'}</caption>
<Select bind:value={value3} outlined autocomplete {label} {items} />

<p>Custom options slot</p>

<Select
  {selectedLabel}
  outlined
  color="red"
  inputClasses={i => i.replace('rounded-t', 'rounded-full')}
  appendClasses={i => i.replace('text-gray-700', 'text-red-700')}
  label="Categories"
  {items}
>
  <div slot="options" class="elevation-3 rounded px-2 py-4 mt-0" on:click|stopPropagation>
      {#each items as item}
        <Checkbox
          value={selectedItems.includes(item)}
          class="block my-2"
          color="red"
          label={item.text}
          on:change={toggle(item)}
        />
      {/each}
  </div>
</Select>