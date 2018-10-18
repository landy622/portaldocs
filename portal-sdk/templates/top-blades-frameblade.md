## FrameBlade

FrameBlades provide an alternative programming model for developing UI in Ibiza. This alternative gives the extension author full control over the DOM via an IFrame. Fx controls cannot be used within FrameBlades. 

Because Frame blades do not use Ibiza Fx controls, extension developers are fully responsible for accessibility, theming, and consistency.

While this programming model results in maximum flexibility, it  also adds a significant burden of accessibility, theming, and consistency on the developer.   We recommend using Frame blades under the following conditions.

* An existing web experience needs to be migrated to Ibiza without being re-implemented
* An existing web experience needs to be hosted in many environments where Ibiza is just one of the hosts
* Developers want to implement user interactions and experiences that are not supported by Ibiza Framework components. For example, you need to build a very rich, custom UX that is not likely to be reused across services.

When using AppBlade, developers are responsible for the following.

* Accessibility

    Making the blade accessible, as specified in [portalfx-accessibility.md](portalfx-accessibility.md)

* Theming

    The extension's UI should always reflect the user's currently selected theme, and should react dynamically when the user changes themes

* Consistent Look & feel

    Designing a visual experience that is consistent with the rest of Ibiza

* Controls

    Building your own controls, or using available alternatives to Ibiza Fx controls

To create a FrameBlade, you need to create 3 artifacts.

**NOTE**: In this discussion, `<dir>` is the `SamplesExtension\Extension\` directory, and  `<dirParent>`  is the `SamplesExtension\` directory, based on where the samples were installed when the developer set up the SDK. If there is a working copy of the sample in the Dogfood environment, it is also included.

1. Register the FrameBlade with your extension by creating a TypeScript class with the @FrameBlade decorator. The samples extension file for this is located at   `<dir>/Client/V2/Blades/FrameBlade/SampleFrameBlade.ts` and in the following example.

{"gitdown": "include-section", "file":"../Samples/SamplesExtension/Extension/Client/V2/Blades/FrameBlade/SampleFrameBlade.ts", "section": "top-blades-frameblades#viewmodel"}

2. Create an html page that will serve as the main contents of your iframe.  The samples extension file for this is located at `<dir>/Content/SamplesExtension/framebladepage.html` and in the following example.

```html
{"gitdown": "include-file", "file": 
"../Samples/SamplesExtension/Extension/Content/SamplesExtension/framebladepage.html"}
```

3. Create a script that will communicate with your extension by using post messages. This is how your extension can get the auth token, respond to theme changes, and other tasks. The samples extension file for this is located        is located at  `<dir>/Content/Scripts/framepage.js`, and is also in the following example.

```js
{"gitdown": "include-file", "file": 
"../Samples/SamplesExtension/Extension/Content/Scripts/framepage.js"}
```

## Changing UI themes

When using a FrameBlade, extension developers can implement themes. Typically, the user selects a theme, which in turn is sent to the UI IFrame. The following code snippet demonstrates how to pass the selected theme to the UI IFrame using the **postMessage** method.

{"gitdown": "include-section", "file": "../Samples/SamplesExtension/Extension/Client/V1/Blades/AppBlade/ViewModels/AppBladeViewModel.ts", "section": "appBlade#postThemingInfo"}

On the iframe side you can respond to the message just like you would respond to the auth token message. You can then adjust your css accordingly.