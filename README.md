<a href="https://ryanehrler.github.io/ngx-syntax-highlighter/">
  <h1 align="center">ngx-syntax-highlighter</h1>
<a/>
Check it out in action <a href="https://ryanehrler.github.io/ngx-syntax-highlighter/">here.</a>

## Installing

```bash
$ npm install --save ngx-syntax-highlighter
```
## Brief description on Highlight.js
Highlight.js will give you syntax highlighting but will not format your code.  When adding 
syntax styling Highlight.js will auto detect the language based on the current array of 
languages in it's memory.  **This array of languages is configurable**.  It is not recommended
you load ALL languages as there are 185 supported lanuages; however if you don't care about the
binary size you can do this.  **Currently** only one syntax style can be loaded at a single time,
however you can change these on the fly.

<a href="https://highlightjs.org/">More info here on Highlight.js</a>

## Start

Import **NgxHighlightJsModule** module in app.module or core.module.

```typescript
import { NgxHighlightJsModule } from 'ngx-syntax-highlighter'

(...)

@NgModule({
  (...)
  imports: [
    NgxHighlightJsModule.forRoot()
  ]
  (...)
})
```

Or specify options

```typescript
import {
  HighlightJsConfig,
  Language,
  NgxHighlightJsModule,
  SyntaxStyle
  } from 'ngx-syntax-highlighter';

const highlightJsConfig: HighlightJsConfig = {
  style: SyntaxStyle['AN-OLD-HOPE'],
  languages: [Language.TYPESCRIPT, Language.JAVASCRIPT]
  // languages: 'all'
};

@NgModule({
  (...)
  imports: [
    NgxHighlightJsModule.forRoot(highlightJsConfig)
  ]
  (...)
})
```

**HighlightJsConfig**

| property  |                value | description                                                                                                         |
| --------- | -------------------: | :------------------------------------------------------------------------------------------------------------------ |
| style     |                 null | No syntax style specified will use default (GITHUB)                                                                 |
|           | SyntaxStyle['STYLE'] | All supported styles listed in enum. Intellisense will ensure you select a valid style.                             |
|           |                      | ~                                                                                                                   |
| languages |                 null | None specified means you will supply a language later in the component.                                             |
|           |           Language[] | Array of languages which will be loaded on init. Can still specify languages later in component.                    |
|           |                'all' | Will load Highlight.js with all languages. This is the simplest solution but also will generate the largest binary. |

#### More Config Examples
**Note:** Configuring in the Module import is optional.

```typescript
// Style and Language Configured
const highlightJsConfig: HighlightJsConfig = {
  style: SyntaxStyle['AN-OLD-HOPE'],
  languages: [Language.TYPESCRIPT]
};

// Only configure language
const highlightJsConfig: HighlightJsConfig = {
  languages: [Language.TYPESCRIPT]
};

// Only configure style
const highlightJsConfig: HighlightJsConfig = {
  style: SyntaxStyle['AN-OLD-HOPE'],
};

// Load all languages and style
const highlightJsConfig: HighlightJsConfig = {
  style: SyntaxStyle.GITHUB,
  languages: 'all'
};

// In your App.Module or Core.Module
imports: [
  NgxHighlightJsModule.forRoot(highlightJsConfig)
]
```

### Syntax Highlighter Component
To highlight a block of code use the below component in your component.html

```html
<ngx-syntax-highlighter
    [language]="languages.CS"
    [style]="syntaxStyle.VS"
    [code]="csharp"
  ></ngx-syntax-highlighter>
```

OR if you setup the language and style in the module import you can just pass in the code

```html
<ngx-syntax-highlighter [code]="csharp"></ngx-syntax-highlighter>
```

In your component.ts
```typescript

import { Language, SyntaxStyle } from 'ngx-syntax-highlighter';
export class AppComponent {
  syntaxStyle = SyntaxStyle;
  languages = Language;
  csharp = `class Program
      {
          static void Main()
          {
              string[] pets = { "dog", "cat", "bird" };

              // ... Loop with the foreach keyword.
              foreach (var value in pets)
              {
                  Console.WriteLine(value);
              }
          }
      }
    `;
}
```

#### Force Language
If Highlight.js isn't recognizing the correct language or incorrectly recognizing the language, then use the **[forceLanguage]** attribute.  Make sure you also specify the **[language]** too.

```html
<ngx-syntax-highlighter 
  [language]="languages.BASH" 
  [code]="bash" 
  [forceLanguage]="true">
</ngx-syntax-highlighter>
```
