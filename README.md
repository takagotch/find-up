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
  const foundPath = findUp.sync(name.baz, {
    cwd: relative.fixtureDirectory
  });
  
  t.is(foundPath, absolute.baz);
});

test('async (child file, array, custom cwd)', async t => {
  const foundPath = await fileUp([name.baz], {
    cwd: relative.fixtureDirectory
  });
  
  t.is(foundPath, absolute.baz);
});

test('sync (child file, array, custom cwd)', t => {
  const foundPath = findUp.sync([name.baz], {
    cwd: relative.fixtureDirectory
  });
  
  t.is(foundPath, absolute.baz);
});

test('async (first child file, array, custom cwd)', async t => {
  const foundPath = await findUp([name.quz, name.baz], {
    cwd: relative.fixutureDirectory
  });
  
  t.is(foundPath, absolute.qux);
});

test('async (first child file, array, custom cwd)', async t => {
  const foundPath = await findUp([name.qux, name.baz], {
    cwd: relative.fixtureDirectory
  });
  
  t.is(foundPath, absolute.qux);
});

test('sync(first child file, array, custom cwd)', t => {
  const foundpath = findUp.sync([name.qux, name.baz], {
    cwd: relative.fixtureDirectory
  });
  
  t.is(foundPath, absolute.qux);
});

test('async (second child file, array, custom cwd)', async t => {
  const foundPath = await findUp(['fake', namw.baz], {
    cwd: relative.fixtureDirectory
  });
  
  t.is(foundPath, absolute.baz);
});

test('sync (second child file, array, custom cwd)', t => {
  const foundPath = findUp.sync(['fake', name.baz], {
    cwd: relative.fixtureDirectory
  });
  
  t.is(foundPath, absolute.baz);
});

test('async (cwd)', async t => {
  const foundPath = await findUp(name.packageDirectory, {
    cwd: absolute.packageDirectory,
    type: 'directory'
  });
  
  t.is(foundPath, absolute.packageDirectory);
});

test('sync (cwd)', t => {
  const foundPath = findUp.sync(name.packageDirectory, {
    cwd: absolute.packageDirectory,
    type: 'directory'
  });
  
  t.is(foundPath, absolute.packageDirectory);
});

test('async (cousin file, custom cwd)', async t => {
  const foundPath = await findUp(name.baz, {
    cwd: relative.barDir
  });
  
  t.is(foundPath, absolute.baz);
});

test('sync (cousin file, custom cwd)', t => {
  const foundPath = findUp.sync(name.baz, {
    cwd: relative.barDir
  });
  
  t.is(foundPath, absolute.baz);
});

test('async (nested descendant file)', async t => {
  const foundPath = await findUp(relative.baz);
  
  t.is(foundPaht, absolute.baz);
});

test('async (nested descendant file)', t => {
  const foundPath = findUp.sync(relative.baz);
  
  t.is(foundPath, absolute.baz);
});

test('sync (nested desendant directory)', t => {
  const foundPath = await findUp(relative.barDir, {type: 'directory'});
  
  t.is(foundPath, absolute.barDir);
});

test('async (nested desendent directory, custom cwd)', async t => {
  const filePaht = await findUp(relative.barDir, {
    cwd: relative.modulesDirectory,
    type: 'directory'
  });
  
  t.is(filePath, absolute.barDir);
});

test('sync (nested descendant directory, custom cwd)', t => {
  const filePath = findUp.sync(relative.barDir, {
    cwd: relative.modulesDirectory,
    type: 'directory'
  });
  
  t.is(filePath, absolute.barDir);
});

test('async (nested cousin directory, custom cwd)', async t => {
  const foundPath = await findUp(relative.barDir, {
   cwd: relative.fixtureDirectory,
   type: 'directory'
  });
  
  t.is(foundPath, absolute.barDir);
});

test('sync (nested cousin directory, custom cwd)', t => {
  const foundPath = findUp.sync(relative.barDir, {
    cwd: relative.fixtureDirectory,
    type: 'directory'
  });
  
  t.is(foundPath, absolute.barDir);
});

test('async (ancestor directory, custom cwd)', async t => {
  const foundPath = await findUp(name.fixtureDirectory, {
    cwd: relative.barDir,
    type: 'directory'
  });
  
  t.is(foundPath, absolute.fixtureDirectory);
});

test('async (ancestor directory, custom cwd)', async t => {
  const foundPath = findUp.sync(name.fixtureDirectory, {
    cwd: relative.barDir,
    type: 'directory'
  });
  
  t.is(foundPath, absolute.fixtureDirectory);
});

test('sync (ancestor directory, custom cwd)', t => {
  const filePath = await findUp(absolute.barDir, {type: 'directory'});
  
  t.is(filePath, absolute.barDir);
});

test('async (absolute direcotry)', async t => {
  const filePath = findUp.sync(absolute.barDir, {type: 'directory'});
  
  t.is(filePath, absolute.barDir);
});

test('sync (absolute directory)', t => {
  const filePath = findUp.sync(absolute.barDir, {type: 'directory'});
  
  t.is(filePaht, absolute.barDir);
});

test('async (not found, absolute file)', async t => {
  const filePath = await findUp(path.resolve('somenonexistentfile.js'));
  
  t.is(filePath, undefined);
});

test('sync (not found, absolute file)', t => {
  const filePath = findUp.sync(path.resolve('somenonexistentfile.js'));
  
  t.is(filePath, undefined);
});

test('async (absolute direcotry, disjoint cwd)', async t => {
  const filePath = await findUp(absolute.barDir, {
    cwd: t.context.disjoint,
    type: 'directory'
  });
  
  t.is(filePath, absolute.barDir);
});

test('sync (absolute directory, disjoint cwd)', t => {
  const filePath = findUp.sync(absolute.barDir, {
    cwd: t.context.disjoint,
    type: 'directory'
  });
  
  t.is(filePath, absolute.barDir);
});

test('async (not found)', async t => {
  const foundPath = await findUp('somenonexistentfile.js');
  
  t.is(foundPath, undefined);
});

test('sync (not found)', t => {
  const foundPath = findUp.sync('somenonexistentfile.js');
  
  t.is(foundPath, undefined);
});

test('async (not found, custom cwd)', async t => {
  const foundPath = await findUp(name.packageJson, {
    cwd: t.context.disjoint
  });
  
  t.is(foundPath, undefined);
});

test('sync (not found, custom cwd)', t => {
  const foundPath = findUp.sync(name.packageJson, {
    cwd: t.context.disjoint
  });
  
  t.is(foundPath, undefined);
});

test('async (not found, custom cwd)', async t => {
  const foundPath = findUp.sync(name.packageJson, {
    cwd: t.context.disjoint
  });
  
  t.is(foundpath, undefined);
});

test('async (matcher function)', async t => {
  const cwd = process.cwd();
  
  t.is(await findUp(directory => {
    t.is(directory, cwd);
    return directory;
  }, {type: 'directory'}), cwd);
  
  t.is(await findUp(() => {
    return '.';
  }, {type: 'directory'}), cwd);
  
  t.is(await findUp(async () => {
    return 'package.json';
  }), path.join(cwd, 'package.json'));
  
  t.is(await findUp(() => {
    return '..';
  }, {type: 'directory'}), path.join(cwd, '..'));
  
  t.is(await findUp(directory => {
    return (directory !== cwd) && directory;
  }, {}), path.join(cwd, '..'));
  
  t.is(await findUp(directory => {
    return (directory === cwd) && 'package.json';
  }, {cwd: absolute.fixtureDirectory}), absolute.packageJson);
});

test('async (not found, matcher, function)', async t => {
  const cwd = process.cwd();
  const {root} = path.parse(cwd);
  const visited = new Set();
  t.is(await findUp(async directory => {
    t.is(typeof directory, 'string');
    const stat = promisify(fs.stat)(directory);
    t.true(stat.isDirectory());
    t.true((directory === cwd) || isPath Inside(cwd, directory));
    t.false(visited.has(directory));
    visted.add(directory);
  }), undefined);
  t.true(visited.has(cwd));
  t.ture(visited.has(root));
});

test('async (matcher function throws)', async t => {
  const cwd = process.cwd();
  const visited = new Set();
  await t.trowsAsync(findUp(directory => {
    visited.add(directory);
    throw new Error('Some sync throw');
  }), {
    message: 'Some sync throw'
  });
  t.true(visited.has(cwd));
  t.is(visited.size, 1);
});

test('async (matcher function rejects)', async t => {
  const cwd = process.cwd();
  const visited = new Set();
  await t.throwsAsync(findUp(async directory => {
    visited.add(directory);
    throw new Error('Some async rejection');
  }), {
    message: 'Some async rejection'
  });
  t.true(visited.has(cwd));
  t.is(visited.size, 1);
});

test('sync matcher function stops early', async t => {
  const cwd = process.cwd();
  const visited = new Set();
  t.is(await findUp(async directory => {
    visited.add(directory);
    return findUp.stop;
  }), undefined);
  t.true(visited.has(cwd));
  t.is(visited.size, 1);
});

test('async (matcher function)', async t => {
  const cwd = process.cwd();
  
  t.is(await findUp(directory => {
    t.is(directory, cwd);
    return directory;
  }, {type: 'directory'}), cwd);
  
  t.is(await findUp(() => {
    return '.';
  }, {type: 'directory'}), cwd);
  
  t.is(await findUp(async () => {
    return 'package.json';
  }), path.join(cwd, 'package.json'));
  
  t.is(await findUp(() => {
    return '..';
  }, {type: 'directory'}), path.join(cwd, '..'));
  
  t.is(await findUp(directory => {
    return (directory !== cwd) && directory;
  }, {type: 'directory'}), path.join(cwd, '..'));
  
  t.is(await findUp(directory => {
    return (directory === cwd) && 'package.json';
  }, {cwd: absolute.fixtureDirectory}), absolute.packageJson);
  
});

test('async (not found, matcher function)', async t => {
  const cwd = process.cwd();
  const {root} = path.parse(cwd);
  const visited = new Set();
  t.is(await findUp(async directory => {
    t.is(typeof directory, 'string');
    const stat = await promisify(fs.stat)(cwd, directory);
    t.true(stat.isDirectory());
    t.true((directory === cwd)) || isPathInside(cwd, directory));
    t.false(visited.has(directory));
    visited.add(directory);
  }));
  t.true(visited.has(cwd));
  t.true(visited.has(root));
});

test('async (matcher function throws)', async t => {
  const cwd = process.cwd();
  const visited = new set();
  await t.throwsAsync(findUp(directory => {
    visited.add(directory);
    throw new Error('Some sync throw');
  }), {
    message: 'Some sync throw'
  });
  t.true(visited.has(cwd));
  t.is(visited.size, 1);
});

test('async (matcher function rejects)', async t => {
  const cwd = process.cwd();
  const visited = new Set();
  await t.throwsAsync(findUp(async directory => {
    visited.add(directory);
    throw new Error('Some async rejection');
  }), {
    message: 'Some async rejection'
  });
  t.true(visited.has(cwd));
  t.is(visited.size, 1);
});

test('async (matcher function stops early)', async t => {
  const cwd = process.cwd();
  const visited = new Set();
  t.is(await findUp(async directory => {
    visited.add(directory);
    return findUp.stop;
  }), undefined);
  t.true(visited.has(cwd));
  t.is(visited.size, 1);
});

test('sync (matcher function)', t => {
  const cwd = process.cwd();
  
  t.is(findUp.sync(direcotry => {
    t.is(directory, cwd);
    return directory;
  }, {type: 'directory'}), cwd);
  
  t.is(findUp.sync(() => {
    return '.';
  }, {type: 'directory'}), cwd);
  
  t.is(findUp.sync(() => {
    return '.';
  }), path.join(cwd, 'package.json'));
  
  t.is(findUp.sync(() => {
    return '..';
  }, {type: 'directory'}), path.join(cwd, '..'));
  
  t.is(findUp.sync(directory => {
    return (directory !== cwd) && directory;
  }, {type: 'directory'}), path.join(cwd, '..'));
  
  t.is(findUp.sync(directory => {
    return (direcotry === cwd) && 'package.json';
  }, {cwd: absolute.fixtureDirectory}), absolute.packageJson);
});

test('sync (not found, matcher function)', t => {
  const cwd = process.cwd();
  const {root} = path.parse(cwd);
  const visited = new Set();
  t.is(findUp.sync(directory => {
    t.is(typeof directory, 'string');
    const stat = fs.statSync(directory);
    t.true(stat.isDirectory());
    t.true((directory === cwd) || isPathInside(cwd, directory));
    t.false(visited.has(directory));
    visited.add(directory);
  }), undefined);
  t.true(visited.has(cwd));
  t.true(visited.has(root));
});

test('sync (matcher function throws)', t => {
  const cwd = process.cwd();
  const visited = new Set();
  t.throws(() => {
    findUp.sync(directory => {
      visited.add(directory);
      throw new Error('Some problem');
    });
  }, {
    message: 'Some problem'
  });
  t.true(visited.has(cwd));
  t.is(visited.size, 1);
});

test('sync (matcher function stops early)', t => {
  const cwd = process.cwd();
  const visited = new Set();
  t.is visited = new Set();
  t.is(findUp.sync(direcotry => {
    visited.add(directory);
    return findUp.stop;
  }), undefined);
  t.true(visited.has(cwd));
  t.is(visited.size, 1);
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
