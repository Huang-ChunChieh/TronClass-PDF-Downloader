```
.
├── content_script.js
├── event.js
└── manifest.json

```

## Explanation

<details open>
<summary>content_script.js</summary>

```javascript
window.open(decodeURIComponent(document.getElementById('pdf-viewer').src.split('?file=')[1]));
```
  1. **Get the element**
      * Use **document.getElementById** method to get the element with the id 'pdf-viewer'
  2. **Get the src attribute of the element**
      * Retrieves **src** attribute value of the element(the URL loaded in the element)
  3. **Split the URL string**
      * Split URL string using **split('?file=')** into two parts and takes the second part (the part at index 1).
      * For example, if the src attribute is:
      ```perl
      /note-bene/pdf-viewer?file=https%3A%2F%2F......
      ```
      * After **split('?file=')**, the array will be:
      ```javascript
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

```javascript
chrome.action.onClicked.addListener((tab) => {
  chrome.scripting.executeScript({
    target: { tabId: tab.id, allFrames: true },
    files: ['content_script.js'],
  });
});
```

  1. **Add a listener for the extension icon click event**
      * When the user clicks the extension icon, this listener is triggered and executes the callback function. The callback function receives a **tab** object representing the currently active tab.
```javascript
chrome.action.onClicked.addListener((tab) => {});
```

  2. **Execute the script:**
      * Use **chrome.scripting.executeScript** method to execute a script in the specified tab. 
```javascript
  chrome.scripting.executeScript({
    target: { tabId: tab.id, allFrames: true },
    files: ['content_script.js'],
  });
```
**The parameters are as follows:**
```javascript
target: { tabId: tab.id, allFrames: true }:
```
**tabId: tab.id** : Specifies that the script should be executed in the currently active tab, as provided by the click event's tab.id.

**allFrames: true** : Indicates that the script should be executed in all frames (including iframes) of the tab.

```javascript
files: ['content_script.js']
```
**files: []** : Specifies the script file to be executed
</details>

<details open>
<summary>manifest.json</summary>

```javascript
{
  "manifest_version": , => The version of the manifest file
  "name": "", => The name of the extension
  "version": "", => The version number of the extension(幫助用戶和開發者瞭解擴充功能的變更)
  "description": "", => Description of the extension
  "icons": { => Logo of the extenison
    "16": "icon16.png",
    "32": "icon32.png",
    "48": "icon48.png",
    "128": "icon128.png"
  },
  "action": { => Defines the action displayed in the toolbar
    "default_title": "" => The default title displayed when the user hovers over the extension icon
  },
  "background": { => Defines the background script for the extension
    "service_worker": "" => The entry file for the background script
  },
  "permissions": ["activeTab", "scripting"] =>Defines the permissions required by the extension(Array)
  "activeTab" => Allows the extension to access the content of the currently active tab
  "scripting" => Allows the extension to execute scripts in web pages
}
```

</details>
