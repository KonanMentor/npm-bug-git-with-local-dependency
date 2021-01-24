## Environment

```sh
$ npm -v
6.14.8
$ node -v
v10.23.0
```

## How to reproduce the bug

Install a package that has `file` dependency (e.g. [this](https://github.com/KonanMentor/npm-package-with-local-dependency/tree/633bf9d3451f48de1f6f6d10ecb9a759a483ac4e) one) as `git` dependency.

```sh
$ npm i 'git+ssh://git@github.com:KonanMentor/npm-package-with-local-dependency.git#633bf9d3451f48de1f6f6d10ecb9a759a483ac4e'
```

### Actual result

Installation fails with

```
npm ERR! code ENOLOCAL
npm ERR! Could not install from "/home/user/npm-bug-git-with-local-dependency, /home/user/npm-bug-git-with-local-dependency/node_modules/npm-package-with-local-dependency/local-dependency" as it does not contain a package.json file.
```

### Expected result

npm sucessfully installs `npm-package-with-local-dependency` as git dependency and links `local-dependency` dependency.

<details>
  <summary>loglevel=silly logs</summary>
  <p>

  ```sh
  $ npm i --loglevel=silly 'git+ssh://git@github.com:KonanMentor/npm-package-with-local-dependency.git#633bf9d3451f48de1f6f6d10ecb9a759a483ac4e'
  npm info it worked if it ends with ok
  npm verb cli [ '/home/user/.nvm/versions/node/v10.23.0/bin/node',
  npm verb cli   '/home/user/.nvm/versions/node/v10.23.0/bin/npm',
  npm verb cli   'i',
  npm verb cli   '--loglevel=silly',
  npm verb cli   'git+ssh://git@github.com:KonanMentor/npm-package-with-local-dependency.git#633bf9d3451f48de1f6f6d10ecb9a759a483ac4e' ]
  npm info using npm@6.14.8
  npm info using node@v10.23.0
  npm verb npm-session 2e5bb4758c3903a8
  npm sill install loadCurrentTree
  npm sill install readLocalPackageData
  npm sill pacote git manifest for undefined@git+ssh://git@github.com/KonanMentor/npm-package-with-local-dependency.git#633bf9d3451f48de1f6f6d10ecb9a759a483ac4e fetched in 2224ms
  npm timing stage:loadCurrentTree Completed in 2263ms
  npm sill install loadIdealTree
  npm sill install cloneCurrentTreeToIdealTree
  npm timing stage:loadIdealTree:cloneCurrentTree Completed in 1ms
  npm sill install loadShrinkwrap
  npm timing stage:loadIdealTree:loadShrinkwrap Completed in 1ms
  npm sill install loadAllDepsIntoIdealTree
  npm sill resolveWithNewModule npm-package-with-local-dependency@1.0.0 checking installable status
  npm sill fetchPackageMetaData error for local-dependency@file:local-dependency Could not install from "/home/user/npm-bug-git-with-local-dependency, /home/user/npm-bug-git-with-local-dependency/node_modules/npm-package-with-local-dependency/local-dependency" as it does not contain a package.json file.
  npm timing stage:rollbackFailedOptional Completed in 1ms
  npm timing stage:runTopLevelLifecycles Completed in 2279ms
  npm sill saveTree npm-bug-git-with-local-dependency@1.0.0
  npm sill saveTree └── npm-package-with-local-dependency@1.0.0
  npm verb stack Error: ENOENT: no such file or directory, open '/home/user/npm-bug-git-with-local-dependency/node_modules/npm-package-with-local-dependency/local-dependency/package.json'
  npm verb cwd /home/user/npm-bug-git-with-local-dependency
  npm verb Linux 5.6.0-1-amd64
  npm verb argv "/home/user/.nvm/versions/node/v10.23.0/bin/node" "/home/user/.nvm/versions/node/v10.23.0/bin/npm" "i" "--loglevel=silly" "git+ssh://git@github.com:KonanMentor/npm-package-with-local-dependency.git#633bf9d3451f48de1f6f6d10ecb9a759a483ac4e"
  npm verb node v10.23.0
  npm verb npm  v6.14.8
  npm ERR! code ENOLOCAL
  npm ERR! Could not install from "/home/user/npm-bug-git-with-local-dependency, /home/user/npm-bug-git-with-local-dependency/node_modules/npm-package-with-local-dependency/local-dependency" as it does not contain a package.json file.
  npm verb exit [ 1, true ]
  npm timing npm Completed in 2635ms
  ```
  </p>
</details>
