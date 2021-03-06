
* `filename` {string} 工作线程主脚本的路径。必须是以 `./` 或 `../` 开头的绝对路径或相对路径（即相对于当前工作目录）。
   如果 `options.eval` 为 `true`，则这是一个包含 JavaScript 代码而不是路径的字符串。
* `options` {Object}
  * `env` {Object} 如果设置，则指定工作线程中 `process.env` 的初始值。
     作为一个特殊值，[`worker.SHARE_ENV`] 可以用于指定父线程和子线程应该共享它们的环境变量。
     在这种情况下，对一个线程的 `process.env` 对象的更改也会影响另一个线程。
     **默认值:** `process.env`。
  * `eval` {boolean} 如果为 `true`，则将构造函数的第一个参数解释为工作线程联机后执行的脚本。
  * `execArgv` {string[]} 传递给工作线程的 node CLI 选项的列表。
     不支持 V8 选项（例如 `--max-old-space-size`）和影响进程的选项（例如 `--title`）。
     如果设置，则它将会作为工作线程内部的 [`process.execArgv`] 提供。
     默认情况下，选项将会从父线程继承。
  * `stdin` {boolean} 如果将其设置为 `true`，则 `worker.stdin` 将会提供一个可写流，其内容将会在工作线程中以 `process.stdin` 出现。
     默认情况下，不提供任何数据。
  * `stdout` {boolean} 如果将其设置为 `true`，则 `worker.stdout` 将不会自动地通过管道传递到父线程中的 `process.stdout`。
  * `stderr` {boolean} 如果将其设置为 `true`，则 `worker.stderr` 将不会自动地通过管道传递到父线程中的 `process.stderr`。
  * `workerData` {any} 能被克隆并作为 [`require('worker_threads').workerData`] 的任何 JavaScript 值。
     克隆将会按照 [HTML 结构化克隆算法][HTML structured clone algorithm]中描述的进行，如果对象无法被克隆（例如，因为它包含 `function`），则会抛出错误。

