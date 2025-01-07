# Use gitreleaser programmatically

From Node.js scripts, gitreleaser can also be used as a dependency:

```js
import release from 'gitreleaser';

release(options).then(output => {
  console.log(output);
  // { version, latestVersion, name, changelog }
});
```
