# Ruby

### Linux编译安装

  #### 步骤
  ```
  # ./configure
  # make
  # make install
  ```
  `gem install` 时遇到
  ```
  ERROR:  Loading command: install (LoadError)
          cannot load such file -- zlib
  ERROR:  While executing gem ... (NoMethodError)
      Underfined method `invoke_with_build_args` for nil:NilClass
  ```
  ```
  ERROR:  While executing gem ... (Gem::Exception)
      Unable to require openssl, install OpenSSL and rebuild Ruby (preferred) or use non-HTTPS sources
  ```

  #### 解决办法
  1. 安装 `openssl` 并使用 `whereis` 命令查看安装位置
      > Ubuntu 18.04 使用apt方式安装的路径选择 /usr/bin

      先安装 `libssl-dev`
      ```
      sudo apt-get install libssl-dev
      ```
      再安装 `openssl`
      ```
      cd {ruby源码目录}/ext/openssl
      ruby extconf.rb --with-openssl-dir=/usr/bin
      ```
      然后 `make` 出现报错
      ```
      make: *** No rule to make target '/include/ruby.h', needed by 'ossl.o'.  Stop.
      ```
      报错的意思就是找不到 `ruby.h` 文件

      其实是 `Makefile` 文件中忘了给路径变量 `top_srcdir` 赋值，调用的时候当然就报错了

      修改 `Makefile` 增加 `top_srcdir = ../..`

      然后执行
      ```
      # make
      # make install
      ```
      完成安装

  1. 安装 `zlib`

      先安装 `zlib1g-dev`
      ```
      # apt-get install zlib1g-dev
      ```
      进入 `ruby` 目录
      ```
      cd {ruby源码目录}/ext/zlib
      ruby extconf.rb
      ```
      然后 `make` 出现报错
      ```
      make: *** No rule to make target '/include/ruby.h', needed by 'zlib.o'.  Stop.
      ```
      解决方法同上

  #### 参考
  <https://blog.csdn.net/colin5300/article/details/42419935>

  <https://blog.csdn.net/pleasurehappy/article/details/72851414>

  <http://samwalt.iteye.com/blog/2371253>
  
  <http://seoaqua.com/ruby-2.1-openssl/>