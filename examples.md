
I only searched for `Object.keys().length`, since that is the most common one.

#### Angular

- https://github.com/angular/angular/blob/7499b74d7d2d6db132d1b19a73e13cf6e306e41e/packages/router/src/url_tree.ts#L119
- https://github.com/angular/angular/blob/7499b74d7d2d6db132d1b19a73e13cf6e306e41e/packages/core/src/transfer_state.ts#L120
- https://github.com/angular/angular/blob/7499b74d7d2d6db132d1b19a73e13cf6e306e41e/packages/compiler/src/render3/view/i18n/util.ts#L57
- https://github.com/angular/angular/blob/7499b74d7d2d6db132d1b19a73e13cf6e306e41e/packages/core/src/util/ng_dev_mode.ts#L97

And multiple more.

#### React

- https://github.com/facebook/react/blob/254dc4d9f37eb512d4ee8bad6a0fae7ae491caef/packages/shared/shallowEqual.js#L33C9-L35
- https://github.com/facebook/react/blob/254dc4d9f37eb512d4ee8bad6a0fae7ae491caef/packages/react-devtools-shared/src/hydration.js#L97
- https://github.com/facebook/react/blob/254dc4d9f37eb512d4ee8bad6a0fae7ae491caef/packages/react-reconciler/src/ReactFiberHydrationDiffs.js#L416-L417
- https://github.com/facebook/react/blob/254dc4d9f37eb512d4ee8bad6a0fae7ae491caef/packages/react-reconciler/src/ReactFiber.js#L677
- https://github.com/facebook/react/blob/254dc4d9f37eb512d4ee8bad6a0fae7ae491caef/packages/react-server/src/ReactFizzServer.js#L2384
- https://github.com/facebook/react/blob/254dc4d9f37eb512d4ee8bad6a0fae7ae491caef/packages/react-dom-bindings/src/client/ReactDOMComponent.js#L3138

#### Node.js

- https://github.com/nodejs/node/blob/c3b6f949748b49ef25b0239bd4582d29976fdbad/lib/internal/util/comparisons.js#L385
- https://github.com/nodejs/node/blob/c3b6f949748b49ef25b0239bd4582d29976fdbad/lib/internal/util/comparisons.js#L754-L763
- https://github.com/nodejs/node/blob/c3b6f949748b49ef25b0239bd4582d29976fdbad/lib/internal/util/comparisons.js#L713-L720 (could be rewritten in a more performant way with the new API)
- https://github.com/nodejs/node/blob/c3b6f949748b49ef25b0239bd4582d29976fdbad/lib/internal/debugger/inspect_client.js#L248
- https://github.com/nodejs/node/blob/c3b6f949748b49ef25b0239bd4582d29976fdbad/lib/internal/cluster/primary.js#L146
- https://github.com/nodejs/node/blob/c3b6f949748b49ef25b0239bd4582d29976fdbad/lib/internal/console/constructor.js#L537

#### Minimatch

https://github.com/isaacs/minimatch/blob/0569cd3373408f9d701d3aab187b3f43a24a0db7/src/index.ts#L158

#### Vue

- https://github.com/vuejs/core/blob/d65b25cdda4c0e7fe8b51e000ecc3696baad0492/packages/shared/src/looseEqual.ts#L36C11-L37
- https://github.com/vuejs/core/blob/d65b25cdda4c0e7fe8b51e000ecc3696baad0492/rollup.config.js#L251
- https://github.com/vuejs/core/blob/d65b25cdda4c0e7fe8b51e000ecc3696baad0492/packages/compiler-core/src/utils.ts#L505
- https://github.com/vuejs/core/blob/d65b25cdda4c0e7fe8b51e000ecc3696baad0492/packages/runtime-core/src/customFormatter.ts#L123
- https://github.com/vuejs/core/blob/d65b25cdda4c0e7fe8b51e000ecc3696baad0492/packages/compiler-sfc/src/style/pluginScoped.ts#L33
- https://github.com/vuejs/core/blob/d65b25cdda4c0e7fe8b51e000ecc3696baad0492/packages/compiler-core/src/transforms/transformElement.ts#L905

#### Lodash

Lodash uses an own implementation that behaves as Object.keys()

- https://github.com/lodash/lodash/blob/8a26eb42adb303f4adc7ef56e300f14c5992aa68/dist/lodash.js#L9921
- https://github.com/lodash/lodash/blob/8a26eb42adb303f4adc7ef56e300f14c5992aa68/dist/lodash.js#L11561

#### Other popular ones

Almost all popular JS/TS modules make use of this pattern.

- https://github.com/trekhleb/javascript-algorithms/blob/e40a67b5d1aaf006622a90e2bda60043f4f66679/src/algorithms/graph/detect-cycle/detectDirectedCycle.js#L83
- https://github.com/storybookjs/storybook/blob/b91e25a25c8c1cc77ea6b316d03b4cce183d815c/code/core/src/theming/ensure.ts#L15
- https://github.com/storybookjs/storybook/blob/b91e25a25c8c1cc77ea6b316d03b4cce183d815c/code/core/src/theming/ensure.ts#L15
- https://github.com/storybookjs/storybook/blob/b91e25a25c8c1cc77ea6b316d03b4cce183d815c/code/lib/blocks/src/blocks/Controls.tsx#L60-L63
- https://github.com/storybookjs/storybook/blob/b91e25a25c8c1cc77ea6b316d03b4cce183d815c/scripts/sandbox/templates/root.ejs#L7
- https://github.com/storybookjs/storybook/blob/b91e25a25c8c1cc77ea6b316d03b4cce183d815c/code/lib/blocks/src/blocks/DocsPage.tsx#L15
- https://github.com/storybookjs/storybook/blob/b91e25a25c8c1cc77ea6b316d03b4cce183d815c/code/core/assets/server/template.ejs#L67
- https://github.com/tailwindlabs/tailwindcss/blob/e8715d081eac683d002892b8b3e13550f0276b45/packages/tailwindcss/src/compat/theme-variants.ts#L9
- https://github.com/tailwindlabs/tailwindcss/blob/e8715d081eac683d002892b8b3e13550f0276b45/packages/%40tailwindcss-upgrade/src/migrate-postcss.ts#L346
- https://github.com/tailwindlabs/tailwindcss/blob/e8715d081eac683d002892b8b3e13550f0276b45/packages/tailwindcss/src/compat/apply-compat-hooks.ts#L100
- https://github.com/puppeteer/puppeteer/blob/ff74c58464f985253b0a986f5fbbe4edc1658a42/packages/puppeteer-core/src/bidi/HTTPRequest.ts#L149
- https://github.com/puppeteer/puppeteer/blob/ff74c58464f985253b0a986f5fbbe4edc1658a42/packages/puppeteer-core/src/bidi/Page.ts#L623
- https://github.com/excalidraw/excalidraw/blob/e1bb59fb8f115cd8e75fcaaeefa03a81b0fdc697/packages/excalidraw/actions/actionSelectAll.ts#L50
- https://github.com/excalidraw/excalidraw/blob/e1bb59fb8f115cd8e75fcaaeefa03a81b0fdc697/packages/excalidraw/change.ts#L133
- https://github.com/excalidraw/excalidraw/blob/e1bb59fb8f115cd8e75fcaaeefa03a81b0fdc697/packages/excalidraw/groups.ts#L38
- https://github.com/excalidraw/excalidraw/blob/e1bb59fb8f115cd8e75fcaaeefa03a81b0fdc697/packages/excalidraw/components/App.tsx#L2760
- https://github.com/excalidraw/excalidraw/blob/e1bb59fb8f115cd8e75fcaaeefa03a81b0fdc697/packages/excalidraw/actions/actionProperties.tsx#L1038
- https://github.com/excalidraw/excalidraw/blob/e1bb59fb8f115cd8e75fcaaeefa03a81b0fdc697/packages/excalidraw/clipboard.ts#L317
- https://github.com/excalidraw/excalidraw/blob/e1bb59fb8f115cd8e75fcaaeefa03a81b0fdc697/packages/excalidraw/element/mutateElement.ts#L44
- https://github.com/microsoft/vscode/blob/2e6728cc3b6ab7f2bc5223dd52abb5f3b595b827/src/vs/base/common/equals.ts#L87-L91
- https://github.com/microsoft/vscode/blob/2e6728cc3b6ab7f2bc5223dd52abb5f3b595b827/src/vs/platform/policy/common/policy.ts#L37
- https://github.com/microsoft/vscode/blob/2e6728cc3b6ab7f2bc5223dd52abb5f3b595b827/build/lib/util.ts#L37
- https://github.com/microsoft/vscode/blob/2e6728cc3b6ab7f2bc5223dd52abb5f3b595b827/src/vs/platform/policy/node/nativePolicyService.ts#L26
- https://github.com/microsoft/vscode/blob/2e6728cc3b6ab7f2bc5223dd52abb5f3b595b827/extensions/terminal-suggest/src/fig/shared/utils.ts#L165
- https://github.com/microsoft/vscode/blob/2e6728cc3b6ab7f2bc5223dd52abb5f3b595b827/build/lib/i18n.ts#L90
- https://github.com/microsoft/vscode/blob/2e6728cc3b6ab7f2bc5223dd52abb5f3b595b827/src/vs/platform/product/common/product.ts#L61
- https://github.com/sveltejs/svelte/blob/f498a21063894e6e515e62d753396410624b2e0f/packages/svelte/src/compiler/phases/3-transform/client/visitors/shared/component.js#L259
- https://github.com/mrdoob/three.js/blob/b0805c2a0fd46c137d605ba098bc2b17d507b46f/src/materials/ShaderMaterial.js#L359
- https://github.com/mrdoob/three.js/blob/b0805c2a0fd46c137d605ba098bc2b17d507b46f/editor/js/Sidebar.Geometry.BufferGeometry.js#L60
- https://github.com/mrdoob/three.js/blob/b0805c2a0fd46c137d605ba098bc2b17d507b46f/examples/jsm/loaders/3MFLoader.js#L239
- https://github.com/vercel/next.js/blob/5c5875105af06e17ccad4080a6ace137f14cdabb/packages/next/src/build/babel/loader/get-config.ts#L177
- https://github.com/vercel/next.js/blob/5c5875105af06e17ccad4080a6ace137f14cdabb/turbopack/packages/devlow-bench/src/cli.ts#L34
- https://github.com/vercel/next.js/blob/5c5875105af06e17ccad4080a6ace137f14cdabb/packages/next/check-error-codes.js#L31
- https://github.com/vercel/next.js/blob/5c5875105af06e17ccad4080a6ace137f14cdabb/scripts/trace-dd.mjs#L67
- https://github.com/vercel/next.js/blob/5c5875105af06e17ccad4080a6ace137f14cdabb/packages/next/src/server/lib/utils.ts#L243
- https://github.com/vercel/next.js/blob/5c5875105af06e17ccad4080a6ace137f14cdabb/scripts/trace-to-tree.mjs#L147
