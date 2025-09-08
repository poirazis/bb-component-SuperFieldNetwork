<script>
  import { getContext, onDestroy } from "svelte";
  import {
    CellString,
    SuperField,
    SuperButton,
  } from "@poirazis/supercomponents-shared";
  import ipaddr from "ipaddr.js";
  import { Cidr, IpAddress } from "cidr-calc";

  const component = getContext("component");
  const allContext = getContext("context");

  const { styleable, enrichButtonActions, Provider, builderStore } =
    getContext("sdk");
  const formContext = getContext("form");
  const formStepContext = getContext("form-step");
  const groupLabelPosition = getContext("field-group");
  const labelWidth = getContext("field-group-label-width");
  const groupColumns = getContext("field-group-columns");
  const groupDisabled = getContext("field-group-disabled");
  const formApi = formContext?.formApi;

  // Field properties
  export let field = "Network Field";
  export let label;
  export let helpText;
  export let span = 6;
  export let placeholder;
  export let defaultValue;
  export let disabled;
  export let readonly;
  export let validation;
  export let invisible = false;
  export let onChange;
  export let debounced;
  export let debounceDelay;
  export let icon;
  export let suggestions;
  export let clearValueIcon;
  export let buttons = [];
  export let autofocus;
  export let labelPosition;

  // Form field state
  let formField;
  let formStep;
  let fieldState = {};
  let fieldApi;
  let fieldSchema;
  let value;
  let parseError;

  // Initialize form step
  $: formStep = formStepContext ? $formStepContext || 1 : 1;
  $: labelPos =
    groupLabelPosition && labelPosition == "fieldGroup"
      ? groupLabelPosition
      : labelPosition;

  // Register field with form
  $: formField = formApi?.registerField(
    field,
    "string",
    defaultValue,
    disabled,
    readonly,
    validation,
    formStep
  );

  // Subscribe to field state changes
  $: unsubscribe = formField?.subscribe((value) => {
    fieldState = value?.fieldState || {};
    fieldApi = value?.fieldApi;
    fieldSchema = value?.fieldSchema;
  });

  // Update value from field state
  $: value = fieldState?.value !== undefined ? fieldState.value : defaultValue;
  $: error = fieldState?.error;

  // Handle IP/CIDR validation
  $: if (value) {
    parseError = undefined;
    if (ipaddr.isValid(value)) {
      try {
        ipaddr.parse(value);
      } catch (e) {
        parseError = "Invalid IP address";
      }
    } else {
      try {
        ipaddr.parseCIDR(value);
      } catch (error) {
        parseError = "Invalid IP/CIDR format";
      }
    }
  }

  // Cell options for the input
  $: cellOptions = {
    placeholder,
    defaultValue,
    disabled: disabled || groupDisabled,
    readonly: readonly || disabled,
    padding: "0.5rem",
    icon,
    clearValueIcon,
    error: fieldState.error || parseError,
    role: "formInput",
    debounce: debounced ? debounceDelay || 300 : false,
    ...(suggestions && { suggestions }),
  };

  // Handle value changes
  const handleChange = (newValue) => {
    onChange?.({ value: newValue });
    fieldApi?.setValue(newValue);
  };

  // Cleanup on component destroy
  onDestroy(() => {
    fieldApi?.deregister?.();
    unsubscribe?.();
  });

  // Component styles
  $: $component.styles = {
    ...$component.styles,
    normal: {
      ...$component.styles.normal,
      display:
        invisible && !$builderStore.inBuilder
          ? "none"
          : $component.styles.normal.display,
      opacity: invisible && $builderStore.inBuilder ? 0.6 : 1,
      "grid-column": groupColumns ? `span ${span}` : "span 1",
    },
  };
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<!-- svelte-ignore a11y-no-noninteractive-tabindex -->
<div use:styleable={$component.styles}>
  <Provider data={{ value }} />
  <SuperField {labelPos} {labelWidth} {field} {label} {error} {helpText}>
    <CellString
      {cellOptions}
      {value}
      {fieldSchema}
      {autofocus}
      on:change={(e) => handleChange(e.detail)}
    />
    {#if buttons?.length}
      <div class="inline-buttons">
        {#each buttons as { text, onClick, quiet, type, size }}
          <SuperButton
            {quiet}
            {disabled}
            {size}
            {type}
            {text}
            on:click={enrichButtonActions(onClick, $allContext)}
          />
        {/each}
      </div>
    {/if}
  </SuperField>
</div>
