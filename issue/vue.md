# Vue

### 1. Invalid Host header

#### 原因
> `Webpack` 新增了对 `host header` 的正确性检测，以屏蔽未经授权的访问

#### 解决办法
1. 执行 `webpack-dev-server` 命令时手动添加 `--public` 选项，取值为授权的 host，这是官方建议的做法，目的是为了安全。
1. 设置 `webpack-dev-server` 的配置项 `disableHostCheck` 为 `true` 以禁用这一检测，如果开发者使用了代理，或在开发环境中不 care 这些安全问题，该设置可以直接斩草除根。

#### 例外
1. host 为 localhost 或 127.0.0.1 时不会受阻。
1. 只有使用 webpack-dev-server 或 webpack-dev-middleware 时会进行该项检测，webpack 和 打包后的代码不受此影响。

#### 参考
<https://blog.csdn.net/salmonellavaccine/article/details/75332654>