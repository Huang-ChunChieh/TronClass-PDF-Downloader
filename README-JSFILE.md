```
.
├── content_script.js
├── event.js
└── manifest.json

```

## Explanation

<details open>
<summary>content_script.js</summary>

```bash
window.open(decodeURIComponent(document.getElementById('pdf-viewer').src.split('?file=')[1]));
```
  1. **Get the element**
      * Use **document.getElementById** method to get the element with the id 'pdf-viewer'
  2. **Get the src attribute of the element**
      * Retrieves **src** attribute value of the element(the URL loaded in the element)
  3. **Split the URL string**
      * Split URL string using **split('?file=')** into two parts and takes the second part (the part at index 1).
      * For example, if the src attribute is:
      ```
      /note-bene/pdf-viewer?file=https%3A%2F%2F......
      ```
      * After **split('?file=')**, the array will be:
      ```
      [
      "/note-bene/pdf-viewer",
      "https%3A%2F%2F......" // Index 1 Results
      ]
      ```
  4. **URL decoding**
      * The **decodeURIComponent** function decodes the URL-encoded part, returning the original URL.
  5. **Open the URL in a new window**
      * The **window.open** method opens the decoded URL in a new window
</details>


<details open>
<summary>event.js</summary>

```bash

```

</details>

<details open>
<summary>manifest.json</summary>

```bash

```

</details>
