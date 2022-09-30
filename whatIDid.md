
Astro 사용법

정지현 09/30

https://docs.astro.build/en/install/auto/

// react, svelte, tailwind 사용할 것인가?? -> 일단 사용 안함

// deploy guide 필요한가? 일단 필요없음

// project structure guiode 필요한가? 필요함.

// https://docs.astro.build/en/editor-setup/ vscode 세팅 필요
// lint, prettier
// https://ota-meshi.github.io/eslint-plugin-astro/user-guide/
// prettier는 위 위 url에 있음.

위 url 그대로 따라하기

.eslintrc.js와 ./.vscode/settings.json 추가함.

까는 것 3가지

1. eslint eslint-plugin-astro 린트와 린트 astro plugin
2. @typescript-eslint/parser
3. eslint-plugin-jsx-a11y 

a11y란 ? 웹 접근성을 위한 protocol

// lint 세팅중

// 

https://docs.astro.build/en/core-concepts/project-structure/

Directories and Files
Section titled Directories and Files
Astro leverages an opinionated folder layout for your project. Every Astro project root should include the following directories and files:

src/* - Your project source code (components, pages, styles, etc.)
public/* - Your non-code, unprocessed assets (fonts, icons, etc.)
package.json - A project manifest.
astro.config.mjs - An Astro configuration file. (recommended)
tsconfig.json - A TypeScript configuration file. (recommended)

## pages 폴더

```
---
import MySiteLayout from '../layouts/MySiteLayout.astro';
---
<MySiteLayout>
  <p>My page content, wrapped in a layout!</p>
</MySiteLayout>
```

식으로 layouts에 md 만든 뒤 page.astro에서 부른다.


.md 파일도 불러와서 부를 수 있음

```
---
layout: '../layouts/MySiteLayout.astro'
title: 'My Markdown page'
---
# Title

This is my page, written in **Markdown.**
```

HTML 파일도 그냥 넣어서 그릴 수 있지만, Astro 기능이 제한될 수 있다.

404.astro를 만들어서 에러로 해줄 수 있음.

## layouts 폴더

reusable 한 page template을 만드는 폴더.

위처럼 .astro, .md 포맷을 사용하며, 일반 html태그로 작업함.

md layout은 넘어감.

```
---
import BaseLayout from './BaseLayout.astro'
const {frontmatter} = Astro.props;
---
<BaseLayout>
  <h1>{frontmatter.title}</h1>
  <h2>Post author: {frontmatter.author}</h2>
  <slot />
</BaseLayout>
```

위처럼 composition도 가능하고, {frontmetter}라는 prop을 선언해서 데이터를 받아올 수 있음.

## components 폴더

The most important thing to know about Astro components is that they render to HTML during your build. Even if you run JavaScript code inside of your components, it will all run ahead of time, stripped from the final page that you send to your users. The result is a faster site, with zero JavaScript footprint added by default.

중요한것은, build에서 html을 render하고 js 역시 render 이전에 실행이 완료되므로 더 빠른 실행이 된다.

```
---
// Component Script (JavaScript)
---
<!-- Component Template (HTML + JS Expressions) -->
```
컴포넌트 템플릿

```
---
import Button from './Button.astro';
---
<div>
  <Button title="Button 1" />
  <Button title="Button 2" />
  <Button title="Button 3" />
</div>
```

buttonGroup 안의 Button component composition 예시

---

---
로 astro의 code fence를 만들 수 있음. 

이 안에 js 코드를 넣는다.

```
---
import SomeAstroComponent from '../components/SomeAstroComponent.astro';
import SomeReactComponent from '../components/SomeReactComponent.jsx';
import someData from '../data/pokemon.json';

// Access passed-in component props, like `<X title="Hello, World" />`
const {title} = Astro.props;
// Fetch external data, even from a private API or database
const data = await fetch('SOME_SECRET_API_URL/users').then(r => r.json());
---
<!-- Your template here! -->
```


문법 예시
```
---
// Your component script here!
import ReactPokemonComponent from '../components/ReactPokemonComponent.jsx';
const myFavoritePokemon = [/* ... */];
---
<!-- HTML comments supported! -->

<h1>Hello, world!</h1>

<!-- Use props and other variables from the component script: -->
<p>My favorite pokemon is: {Astro.props.title}</p>

<!-- Include other components with a `client:` directive to hydrate: -->
<ReactPokemonComponent client:visible />

<!-- Mix HTML with JavaScript expressions, similar to JSX: -->
<ul>
  {myFavoritePokemon.map((data) => <li>{data.name}</li>)}
</ul>

<!-- Use a template directive to build class names from multiple strings or even objects! -->
<p class:list={["add", "dynamic", {classNames: true}]} />

```

너무나도 많으니깐, 일단 fullpagejs를 먼저 적용해본다.


1. yarn add fullpage.js 넣음

생각해보니 이게 적용 안될거같음

그래서 index.astro는 일단 백업으로 빼놓고

index.html을 만들어보는게 나을듯