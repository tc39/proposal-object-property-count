Object.getOwnPropertyNames:
- @storybook/core - it needs the number of properties (enumerable + non-enumerable)
- storybook - it needs the number of properties (enumerable + non-enumerable)
- prettier - faster for zero case (it skips )
- hoppscotch - it needs the number of properties (enumerable + non-enumerable)
- grapesjs - it needs the number of properties (enumerable + non-enumerable)
- claude-code-router
- moment (just empty check)
- video.js (just empty check)
- Node.js
- Any babel transpiled code

Object.getOwnPropertySymbols:
- @storybook/core - needs the number of symbols (enumerable + non-enumerable)
- storybook - needs the number of symbols (enumerable + non-enumerable)
- hoppscotch - needs the number of symbols (enumerable + non-enumerable)
- claude-code-router
- ava (fast path in case no symbols)
- Node.js
- Any babel transpiled code

No enumerable:
- Object.getOwnPropertySymbols - filtered out (no enumerable)

rxjs
winston
webpack-dev-server
vue
@storybook/core
excalidraw
storybook
hoppscotch (maybe PDFLensRenderer)
code-server
nocodb
cypress (vue bundled)
angular
prisma
lerna
slate
@uppy/core
nx
recharts
redoc
intro.js
playright (bundled stuff)
react-dnd (bundled stuff)
svelte
tesseract.js
webtorrent
plyr
swagger-ui
ava
tabler-icons
