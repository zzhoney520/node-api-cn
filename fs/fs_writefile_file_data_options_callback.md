<!-- YAML
added: v0.1.29
changes:
  - version: v10.10.0
    pr-url: https://github.com/nodejs/node/pull/22150
    description: The `data` parameter can now be any `TypedArray` or a
                 `DataView`.
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: The `callback` parameter is no longer optional. Not passing
                 it will throw a `TypeError` at runtime.
  - version: v7.4.0
    pr-url: https://github.com/nodejs/node/pull/10382
    description: The `data` parameter can now be a `Uint8Array`.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning with id DEP0013.
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/3163
    description: The `file` parameter can be a file descriptor now.
-->

* `file` {string|Buffer|URL|integer} 文件名或文件描述符。
* `data` {string|Buffer|TypedArray|DataView}
* `options` {Object|string}
  * `encoding` {string|null} **默认值:** `'utf8'`。
  * `mode` {integer} **默认值:** `0o666`。
  * `flag` {string} 参阅[支持的文件系统标志][support of file system `flags`]。**默认值:** `'w'`。
* `callback` {Function}
  * `err` {Error}

当 `file` 是一个文件名时，异步地将数据写入到一个文件，如果文件已存在则覆盖该文件。
`data` 可以是字符串或 buffer。

当 `file` 是一个文件描述符时，行为类似于直接调用 `fs.write()`（建议使用）。 
请参阅以下有关使用文件描述符的说明。

如果 `data` 是一个 buffer，则 `encoding` 选项会被忽略。

```js
const data = new Uint8Array(Buffer.from('Node.js中文网'));
fs.writeFile('文件.txt', data, (err) => {
  if (err) throw err;
  console.log('文件已被保存');
});
```

如果 `options` 是一个字符串，则它指定字符编码：

```js
fs.writeFile('文件.txt', 'Node.js中文网', 'utf8', callback);
```

在同一个文件上多次使用 `fs.writeFile()` 且不等待回调是不安全的。
对于这种情况，建议使用 [`fs.createWriteStream()`]。


