# formily materials

这里是 lowcode engine 的 formily antd 资产包。用于表单搭建, 如果你对 formily 完全陌生，可以[在此](https://v2.formilyjs.org/zh-CN/guide)对 formily 进行快速学习。

## how to use

1. 安装注册插件

```
npm install @seada/antd-plugins
```

```javascript
import { PluginFormily } from '@seada/antd-plugins';
import { plugins } from '@alilc/lowcode-engine';

async function registerPlugins() {
  await plugins.register(PluginFormily);
}

registerPlugins();
```

2. assets.json 中添加资产包

```json
{
  "packages": [
    {
      "package": "@seada/formily-materials",
      "version": "0.1.1",
      "library": "SeadaFormilyMaterials",
      "urls": [
        "https://cdn.jsdelivr.net/npm/@seada/formily-materials@latest/build/lowcode/view.js",
        "https://cdn.jsdelivr.net/npm/@seada/formily-materials@latest/build/lowcode/view.css"
      ],
      "editUrls": [
        "https://cdn.jsdelivr.net/npm/@seada/formily-materials@latest/build/lowcode/view.js",
        "https://cdn.jsdelivr.net/npm/@seada/formily-materials@latest/build/lowcode/view.css"
      ]
    }
  ],
  "components": [
    {
      "exportName": "SeadaFormilyMaterialsMeta",
      "npm": {
        "package": "@seada/formily-materials",
        "version": "0.1.1"
      },
      "url": "https://cdn.jsdelivr.net/npm/@seada/formily-materials@latest/build/lowcode/meta.js",
      "urls": {
        "default": "https://cdn.jsdelivr.net/npm/@seada/formily-materials@latest/build/lowcode/meta.js"
      }
    }
  ]
}
```

> 资产包可以自行构建并上传至你的 cdn，使用时替换链接即可。

## formily expand

为了 lowcode engine 以及 formily 的无缝结合，我们在 formily 中扩展了一些新特性，辅助我们的搭建工作

### formRef

为了在 lowcode engine 的页面 js 中使用 formily，我们为 formily 的 form 增加了 ref 属性，假设我们设置了 formily form 组件的 ref 属性为`formily_name`，那么我们可以在 js 面板中通过`this.$('formily_name').form`获取该表单的[form 实例](https://core.formilyjs.org/zh-CN/api/models/form)。因此，我们可以在 js 面板中使用 formily 的 form 实例进行表单验证，获取/设置表单值。

### $this

为了在 formily 中获取 lowcode engine page 实例的数据，我们在 formily 中注入了`$this`变量，`$this`的使用与 formily 中的`$self`、`$deps`等使用方法相同。`$this`指向 page 实例，我们可以在 formily 组件中使用`$this.state`获取页面的 state，`$this.setState`触发数据更新等任意操作

### VarInjectContainer 组件

为了使普通的 lowcode engine 组件获取一些 formily 组件运行时才会产生的数据，例如 ArrayCards 组件中子项的`$record`，我们新增了`VarInjectContainer`组件。`VarInjectContainer`组件的子元素都可以通过 `this.vars.$record`，`this.vars.$index`等获取 formily 运行时数据。