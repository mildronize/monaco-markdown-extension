
# Monaco Markdown Extension

## Install

```
yarn install monaco-markdown-extension monaco-editor
```

## Usage 

With React (`@monaco-editor/react`)

Do later

With Next.js (https://github.com/vercel/next.js/tree/canary/examples/with-monaco-editor)

```javascript
import dynamic, { noSSR } from 'next/dynamic'
import { useEffect, useState } from 'react'

const MonacoEditor = dynamic(import('react-monaco-editor'), { ssr: false })

const MarkdownEditor = (props) => {

  function importNoSSR(editor) {
    const loader = async () => {
      let MonacoMarkdown = await import('monaco-markdown-extension')
      var extension = new MonacoMarkdown.MonacoMarkdownExtension();
      extension.activate(editor);
    }
    loader();
  }

  function _editorDidMount(editor, monaco) {
    // This come from next.js example
    // @ts-ignore
    window.MonacoEnvironment.getWorkerUrl = (moduleId, label) => {
      if (label === 'json') return '/_next/static/json.worker.js'
      if (label === 'css') return '/_next/static/css.worker.js'
      if (label === 'html') return '/_next/static/html.worker.js'
      if (label === 'typescript' || label === 'javascript')
        return '/_next/static/ts.worker.js'
      return '/_next/static/editor.worker.js'
    }

    // Make sure no ssr part in this extension
    importNoSSR(editor);
  }

  return (
    <>
      <MonacoEditoritor
        language="markdown"
        editorDidMount={_editorDidMount}
      />
    </>

  )
}

export default MarkdownEditor;
```

[Monaco Editor](https://github.com/Microsoft/monaco-editor) 

Thank you typescript & Rollup template from https://github.com/HarveyD/react-component-library

## Ref

- Special thanks ported [Markdown extension for VS Code](https://github.com/yzhang-gh/vscode-markdown) to Monaco web editor.
- [Markdown extension for VS Code](https://github.com/yzhang-gh/vscode-markdown)
