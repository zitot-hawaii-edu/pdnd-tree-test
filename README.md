steps to reproduce without downloading this git repository.

Create a new project using yarn and vite

```yarn create vite```

Give the project a name. 

Pick React and Typescript for the project lang

```cd <project-name>```

Add dependencies using Yarn add

```
yarn add react react-dom @emotion/react tiny-invariant memoize-one;
yarn add @atlaskit/pragmatic-drag-and-drop \
  @atlaskit/pragmatic-drag-and-drop-flourish \
  @atlaskit/pragmatic-drag-and-drop-hitbox \
  @atlaskit/pragmatic-drag-and-drop-live-region \
  @atlaskit/pragmatic-drag-and-drop-react-drop-indicator;
yarn add @atlaskit/tokens @atlaskit/css-reset @atlaskit/ds-lib @emotion/react;
yarn add @atlaskit/button \
  @atlaskit/dropdown-menu \
  @atlaskit/icon \
  @atlaskit/modal-dialog \
  @atlaskit/form \
  @atlaskit/select \
  @atlaskit/focus-ring \
  @atlaskit/app-provider;

```

Change directory and create folders. Use -p to do it all at once

```
mkdir -p src/pragmatic-drag-and-drop/documentation/examples/data
mkdir -p src/pragmatic-drag-and-drop/documentation/examples/pieces/tree
```

Go to [Tree @codesandbox](https://codesandbox.io/p/sandbox/tree-forked-2ntmyh) and copy the files to the appropriate folders. 

Edit main.tsx to load css-reset instead of ./index.css and Example from ./example.tsx instead of the default App.tsx

In tree-item.tsx, remove the old React16 style render logic inside onGenerateDragPreview. Replace it with React 18 style rendering. Don't forget to change the include file at the top to point to react-dom

Change
```import ReactDOM from 'react-dom';``` to ```import { createRoot } from 'react-dom/client';```

And
```
						render: ({ container }) => {
							ReactDOM.render(<Preview item={item} />, container);
							return () => ReactDOM.unmountComponentAtNode(container);
						},
```

to

```
    render: ({ container }) => {
      const root = createRoot(container);
      root.render(<Preview item={item} />);

      // Cleanup on unmount
      return () => root.unmount();
    },
```
### End main Content
# React + TypeScript + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react/README.md) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh

## Expanding the ESLint configuration

If you are developing a production application, we recommend updating the configuration to enable type aware lint rules:

- Configure the top-level `parserOptions` property like this:

```js
export default tseslint.config({
  languageOptions: {
    // other options...
    parserOptions: {
      project: ['./tsconfig.node.json', './tsconfig.app.json'],
      tsconfigRootDir: import.meta.dirname,
    },
  },
})
```

- Replace `tseslint.configs.recommended` to `tseslint.configs.recommendedTypeChecked` or `tseslint.configs.strictTypeChecked`
- Optionally add `...tseslint.configs.stylisticTypeChecked`
- Install [eslint-plugin-react](https://github.com/jsx-eslint/eslint-plugin-react) and update the config:

```js
// eslint.config.js
import react from 'eslint-plugin-react'

export default tseslint.config({
  // Set the react version
  settings: { react: { version: '18.3' } },
  plugins: {
    // Add the react plugin
    react,
  },
  rules: {
    // other rules...
    // Enable its recommended rules
    ...react.configs.recommended.rules,
    ...react.configs['jsx-runtime'].rules,
  },
})
```
# pdnd-example-tree
# pdnd-tree-test
