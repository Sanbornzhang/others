# install
`npm install -g hexo-cli`
# init
`hexo init blog`
# change style
1. find style github
2. cd init folder
3. git clone
4. change config file `_config.yml`
# with pm2
```
index.js

const { spawn } = require('child_process')
let server = spawn('hexo',['server'])
server.stdout.on('data', (data) => {
    console.log(`stdout: ${data}`);
  })
server.stderr.on('data', (data) => {
    console.log(`stderr: ${data}`);
  })
server.on('close', (code) => {
    console.log(`子进程退出码：${code}`);
  });

```
pm2 start index.js

