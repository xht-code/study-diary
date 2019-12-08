# Maven

### 目录
1. [Dependency Optional](#dependency_optional)
    1. [作用](#作用)
    1. [参考](#参考)
1. [Dependency Scope](#dependency_scope)
    1. [作用](#作用-1)
    1. [scope的分类](#scope的分类)
    1. [scope的依赖传递](#scope的依赖传递)
    1. [参考](#参考-1)

### Dependency Optional

  #### 作用
  假如你的 `Project A` 的某个依赖**D**添加了
  ``` xml
  <optional>true</optional>
  ```
  当别人通过 `pom` 依赖 `Project A` 的时候，**D**不会被传递依赖进来

  #### 参考
  <https://blog.csdn.net/zwt0909/article/details/53221252>

### Dependency Scope

  #### 作用
  > 在POM 4中，`<dependency>` 中还引入了 `<scope>` ，它主要管理依赖的部署。

  #### scope的分类
  1. **compile**：默认值 他表示被依赖项目需要参与当前项目的编译，还有后续的测试，运行周期也参与其中，是一个比较强的依赖。打包的时候通常需要包含进去
  1. **test**：依赖项目仅仅参与测试相关的工作，包括测试代码的编译和执行，不会被打包，例如：junit
  1. **runtime**：表示被依赖项目无需参与项目的编译，不过后期的测试和运行周期需要其参与。与 `compile` 相比，跳过了编译而已。例如JDBC驱动，适用运行和测试阶段
  1. **provided**：打包的时候可以不用包进去，别的设施会提供。事实上该依赖理论上可以参与编译，测试，运行等周期。相当于 `compile` ，但是打包阶段做了 `exclude` 操作
  1. **system**：从参与度来说，和 `provided` 相同，不过被依赖项不会从maven仓库下载，而是从本地文件系统拿。需要添加systemPath的属性来定义路径

  #### scope的依赖传递
  A依赖B，B依赖C。当前项目为A，只当B在A项目中的scope，那么c在A中的scope是如何得知呢？

  当C是test或者provided时，C直接被丢弃，A不依赖C；（排除传递依赖）

  否则A依赖C，C的scope继承与B的scope

  #### 参考
  <https://blog.csdn.net/zwt0909/article/details/53221252>
  
  <https://blog.csdn.net/cd18333612683/article/details/66478332>