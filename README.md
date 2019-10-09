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
  const tmpDir = tempy.directory();
  t.context.disjoint = tmpDir;
});

test.afterEach(t => {
  fs.rmdirSync(t.context.disjoint);
});

const isWindows = process.platform === 'win32';

test('async (child file)', async t => {
  const foundPath = await findUp(name.packageJson);
  
  t.is(foundPath, absolute.packageJson);
});

test('sync (child file)', t => {
  const foundPath = findUp.sync(name.packageJson);
  
  t.is(foundPath, absolute.packageJson);
});

test('async (child directory)', async t => {
  const foundPath = await findUp(name, fixtureDirectory, {type: 'directory'});
  
  t.is(foundPath, absolute.fixtureDirectory);
});

test('sync (child directory)', t => {
  const foundPath = findUp.sync(name.fixtureDirectory, {type: 'directory'});
  
  t.is(foundPath, absolute.fixtureDirectory);
});

test('async (explicit type file)', async t => {
  t.is(await findUp(name.packageJson, {type: 'file'}), absolute.packageJson);
  t.is(await findUp(name.packageJson, {type: 'directory'}), undefined);
});

if(!isWindows) {
  test('async (symbolic links)', async t => {
    const cwd = absolute.fixtureDirectory;
    
    t.is(await findUp(name.fileLink, {cwd}), absolute.fileLink);
    t.is(await findUp(name.fileLink, {cwd, allowSymlinks: false}), undefined);
    
    t.is(await findUp(name.directoryLink, {cwd, type: 'directory'}), absolute.directoryLink);
    t.is(await findUp(name.directoryLink, {cwd, type: 'directory', allowSymlinks: false}), undefined);
  });
  
  test('sync (symbolic links)', t => {
    const cwd = absolute.fixtureDirectory;
    
    t.is(findUp.sync(name.fileLink, {cwd}), absolute.fileLink);
    t.is(findUp.sync(name.fileLink, {cwd, allowSymlinks: false}), undefined);
    
    t.is(findUp.sync(name.directoryLink, {cwd, type: 'directory'}), absolute.directoryLink);
    t.is(findUp.sync(name.directoryLink, {cwd, type: 'directory', allowSymlinks: false}), undefined);
  });
}

test('async (child file, custom cwd)', async t => {
  const foundPath = await findUp(name.baz, {
    cwd: relative.fixtureDirectory
  });
  
  t.is(foundPath, absolute.baz);
});

test('sync (child file, custom cwd)', t => {

});

test();

test();

test();

test();

test();

test();

test();

test();

test();

test();

test();

test();
test();

test();

test();

test();

test();

test();

test();

test();

test();
test();

test();

test();

test();

test();

test('', );

test('async (matcher function)', async t => {

});

test('async (not found, matcher function)', async t => {

});

test('async (matcher function throws)', async t => {

});

test('async (matcher function rejects)', async t => {

});

test('async (matcher function stops early)', async t => {

});

test('sync (matcher function)', t => {

});

test('sync (not found, matcher function)', t => {

});

test('sync (matcher function throws)', t => {

});

test('sync (matcher function stops early)', t => {

});

test('async (check if path exists)', async t => {

});

test('async (check if path exists)', async t => {
  if(!isWindows) {
    t.true(await findUp.exists(absolute.directoryLink));
    t.true(await findUp.exists(absolute.fileLink));
  }
  
  t.true(await findUp.exists(absolute.barDir));
  t.true(await findUp.exists(absolute.packageJson));
  t.false(await findUp.exists('fake'));
});

test('sync (check if path exists)', t => {
  if (!isWindows) {
    t.true(findUp.sync.exists(absolute.directoryLink));
    t.true(findUp.sync.exists(absolute.fileLink));
  }
  
  t.true(findUp.sync.exists(absolute.barDir));
  t.true(findUp.sync.exists(absolute.packageJson));
  t.false(findUp.sync.exists('fake'));
});
```

```
```

```
```
