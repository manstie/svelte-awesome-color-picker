<script lang="ts">
	import ColorPicker from 'svelte-awesome-color-picker/ColorPicker.svelte';
	import CirclePickerColorPicker from './_components/circle-picker/ColorPicker.svelte';
	import ChromePickerColorPicker from './_components/chrome-picker/ColorPicker.svelte';
    import { browser } from '$app/env';

    let color = { hex: "#f6f0dc" };

    $: beautifulColor = JSON.stringify(color, null, 2)
        .replaceAll(/("#\w+")/g, '<span style="color: #e6d06c;">$1</span>')
        .replaceAll(/:\s(\d+\.?\d*)/g, ': <span style="color: #ef3b7d;">$1</span>')
        .replaceAll("\":", '"<span style="color: #a77afe;">:</span>')

    $: if(browser) document.documentElement.style
        .setProperty('--bg-color', color.hex);
</script>

# svelte-awesome-color-picker

> _svelte-awesome-color-picker_ is a highly customizable color picker component library with built in keyboard navigation. It is compatible with form libraries.

## Links

- 🌟 [Github repository](https://github.com/Ennoriel/svelte-awesome-color-picker)
- 🌴 [Npm repository](https://www.npmjs.com/package/svelte-awesome-color-picker)
- 🛫 Documentation: coming soon

## Examples

<div class="example-wrapper">
<div class="example-col">

### Default layout

<ColorPicker bind:color />

### Another horizontal layout

<CirclePickerColorPicker bind:color />

### Chrome like layout

<ChromePickerColorPicker bind:color />

</div>
<div class="example-col">

### Color props

<pre class="language-javascript">
    <span style="color: #ef3b7d;">let</span> color <span style="color: #a77afe;">=</span> {@html beautifulColor}
</pre>

</div>
</div>

## install

```shell
npm i -D svelte-awesome-color-picker
```

## Usage

```svelte
<script>
	import ColorPicker from 'svelte-awesome-color-picker/ColorPicker.svelte';

	let color;
</script>

<ColorPicker bind:color />
```

## Api

### props

| props      | type         | Default Value | Usage                                                                                                                     |
| ---------- | ------------ | ------------- | ------------------------------------------------------------------------------------------------------------------------- |
| isAlpha    | `boolean`    | true          | The alpha slider is visible. If set to false <br /> the alpha value provided by the `setColor` method will not be changed |
| isInput    | `boolean`    | true          | The input button is visible. If set to false <br /> the picker will be open by default                                    |
| isOpen     | `boolean`    | false         | The picker is open by default and cannot be closed                                                                        |
| color      | `Color`      | red           | The color object that should be bound to                                                                                  |
| setColor   | `function`   |               | This method should be called to initialize or modify the color value                                                      |
| components | `Components` |               | see below                                                                                                                 |

### css variables

| props           | Default Value | Usage                   |
| --------------- | ------------- | ----------------------- |
| --picker-height | `300px`       | picker & sliders height |
| --slider-width  | `30px`        | sliders width           |
| --picker-width  | `300px`       | picker width            |
| --focus-color   | `red`         | focus color             |

### components

The color picker can be customized with components. The details and props are detailed below. It is easier to copy the library components and tweak it to your needs.

```svelte
<script>
	// imports
	const components = {
		input: Input,
		sliderIndicator: SliderIndicator,
		sliderWrapper: SliderWrapper,
		alphaIndicator: SliderIndicator,
		alphaWrapper: SliderWrapper,
		pickerIndicator: PickerIndicator,
		pickerWrapper: PickerWrapper,
		wrapper: Wrapper
	};
</script>

<ColorPicker bind:color {components} />
```

#### pickerIndicator

Component representing the picker indicator.

- The component should be positioned with `position: absolute;`.
- It should also have the css property `pointer-events: none;`.

Props:

| props | Default Value            | Usage            |
| ----- | ------------------------ | ---------------- |
| pos   | `{x: number, y: number}` | expressed in %   |
| color | `Color`                  | the actual color |

#### sliderIndicator & alphaIndicator

Components representing the (hue) slider and alpha indicators.

It should also have the css property `pointer-events: none;`.

Props:

| props | Default Value | Usage                                           |
| ----- | ------------- | ----------------------------------------------- |
| pos   | `number`      | expressed in %                                  |
| color | `Color`       | respectively the Hue color and the actual color |

#### Input

Component representing the button to open the color picker and a hidden input with the hex value selected by the user

Props:

| props  | Default Value | Usage                                                                          |
| ------ | ------------- | ------------------------------------------------------------------------------ |
| button | `HTMLElement` | this property should be exported from only focusable element of this component |
| color  | `Color`       | the actual color                                                               |
| isOpen | `boolean`     | props that can be toggled on or off to open or close the color picker          |

#### pickerWrapper & sliderWrapper & alphaWrapper

Encapsulates the picker, hue slider and alpha slider. They should define the css properties `width` and `height`.

Props:

| props   | Default Value | Usage                          |
| ------- | ------------- | ------------------------------ |
| focused | `boolean`     | whether the element is focused |

#### wrapper

Encapsulates the whole color picker

Props:

| props   | Default Value    | Usage                                                          |
| ------- | ---------------- | -------------------------------------------------------------- |
| wrapper | `HTMLDivElement` | this property should be exported with the top most DOM element |
| isOpen  | `boolean`        | whether toe color picker is open or not                        |
| isPopup | `boolean`        | whether the color picker is floating or not                    |

<style>
    .example-wrapper {
        display: grid;
        grid-template-columns: 1fr 1fr;
    }
    :global(body) {
        background-color: var(--bg-color);
    }
</style>