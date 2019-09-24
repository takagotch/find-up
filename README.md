### find-up
---
https://github.com/sindresorhus/find-up

```js
// test.js
import fs from 'fs';

const name = {
  packageDirectory: 'find-up',
  packageJson: 'package.json',
  fixtureDirectory: 'fixture',
  moduleDirectory: 'node_modules',
  baz: 'baz.js',
  qux: 'quz.js',
  fileLink: 'file-link',
  direcotryLink: 'directory-link'
};

const relative = {
  fixtureDirecoty: name.fixtureDirectory,
  modulesDirectory: name.modulesDirectory
};
relative.baz = path.join();
relative.qux = path.join();
relative.barDir = path.join();

const absolute = {
  packageDirectory: __dirname
};
absolute.packageJson = path.join();
absolute.fixtureDirectory = path.join(
  absolute.packageDirectory,
  name.fixtureDirectory
);
absolute.baz = path.join(absolute.fixtureDirectory, name.baz);
absolute.qux = path.join(absolute.fixtureDirectory, name.qux);
absolute.barDir = path.join();
absoute.fileLink = path.join();
absolute.directoryLink = path.join();

test.beforeEach(t => {

});


```

```
```

```
```
