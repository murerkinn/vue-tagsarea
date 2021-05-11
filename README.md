![vue-tagsarea](https://user-images.githubusercontent.com/57751146/117993042-0eaa6f80-b348-11eb-881c-409c59c6a474.png)

vue-tagsarea — A textarea component with tags for Vue.js
====

## Features
- **Auto-splitting:** With auto-splitting feature you can copy a text and split it into tags by just pasting it
- **Preventing duplication of existing tags:** This feature prevents you from having duplicate tags by skipping them, it also highlights the existing ones
- **Built in bootstrap themes:** Built in tags have all the bootstrap themes, you can easily use one with the theme prop

<br>
<center>
<img src="https://cdn.discordapp.com/attachments/678445122630975508/841766827814027284/May-11-2021_22-59-16.gif" />
</center>
<br>

## Table of Contents
1. [Getting started](#getting-started)
1. [API (Props)](#api)
1. [Contribution](#contribution)
1. [License](#mit-license)

Getting Started
----
### Installation

vue-tagsarea is a Node.js library for implementing tags in a textarea easily in your Vue.js applications.

Install vue-tagsarea locally via npm:

```bash
npm install vue-tagsarea
```
### Using vue-tagsarea with built in tags
```js
<template>
  // you can either use vue-tagsarea with an array
  <vue-tagsarea v-model="tagsAsArray" />

  // or with a string and a seperator to split the string. seperator is "\n" by default.
  <vue-tagsarea v-model="tagsAsString" seperator="," />
</template>

<script>
  import VueTagsarea from 'vue-tagsarea';

  export default {
    name: 'YourComponent',
    components: {
      VueTagsarea,
    },
    data() {
      return {
        tagsAsArray: ['tag1', 'tag2', 'tag3'],
        tagsAsString: 'tag1,tag2,tag3',
      };
    },
  };
</script>
```

### Using vue-tagsarea with your own tag component
vue-tagsarea uses named-slots, so you can use your own tag without any difficulty

```js
<template>
  <vue-tagsarea>
    <template v-slot:tag="props">
      <your-custom-tag>{{ props.content }}</your-custom-tag>
    </template>
  </vue-tagsarea>
</template>

<script>
  import VueTagsarea from 'vue-tagsarea';

  export default {
    name: 'YourComponent',
    components: {
      VueTagsarea,
    },
    data() {
      return {
        tags: ['tag1', 'tag2', 'tag3'],
      };
    },
  };
</script>
```

Here is the list of props you can use when you want to use your own tag component:
- **content [String]:**  Content of the tag
- **index [Number]:**  Index of the tag
- **exists [Boolean]:**  Is true if you try to enter an existing tag
- **remove [Function]:**  Removes the specified tag
- **update [Function]:** Updates the specified tag

<br>

# API
| Prop           | Type          | Options                                                         | Default                   | Description                                              |
|----------------|---------------|-----------------------------------------------------------------|---------------------------|----------------------------------------------------------|
| v-model(value) | Array \| String | Your tags as array or string                                    | -                         |                                                          |
| seperator      | String        | any character                                                   | \n                      | Seperator to split the given string into tags            |
| theme          | String        | primary \| secondary \| success \| danger \| warning \| info \| dark \| light | primary                 | Built in Bootstrap themes                                |
| showRemoveAll  | Boolean       | true \| false                                                     | false                     | Adds a remove all tag that removes all the tags on click |
| placeholder    | String        | -                                                               | Enter your tags here... | Placeholder text                                         |
<br>

# Contribution
If you would like to see a feature implemented or want to contribute a new
feature, you are welcome to open an issue to discuss it and we will be more than
happy to help.

If you choose to make a contribution, please fork this repository, work on a
feature and submit a pull request.
<br>
<br>

MIT License
----

Copyright (c) 2021 Murat Erkin Cicek

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
