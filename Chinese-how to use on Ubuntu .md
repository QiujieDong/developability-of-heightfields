# 已验证可以使用

- [Github](https://github.com/QiujieDong/developability-of-heightfields)

- [Original github](https://github.com/sgsellan/developability-of-heightfields/tree/master)

- 需要注意的点：

  - 我验证可以使用的平台是（实验室20年购买的服务器，新的服务器也测试了，会出问题）：
    - Ubuntu 20.04.1 LTS
    - gcc (Ubuntu 8.4.0-3ubuntu2) 8.4.0
    - Cuda compilation tools, release 10.2, V10.2.89
    - RTX 2080 TI
    - 也不知道哪个参数会有影响。

- 首先安装Matlab

  - 安装教程：[无图形界面Linux安装Matlab2020](https://zhuanlan.zhihu.com/p/394298249)
    - 使用教程里的sh安装就可以，很方便
    - 如果教程失效了，可以联系我，或者与上面这个教程的知乎大神联系
  - 安装文成后，将matlab的地址加到zshrc或者bashrc
    - export Matlab_PATH=/home/qiujie/Matlab/R2020a/bin
      export PATH=$Matlab_PATH:$PATH
    - 这样就可以直接在命令行中直接使用matla作为命令
      - 比如可以试一下教程里的测试代码

- 然后按github里面进行cmake就可以

  - 注意：
    - 这里clone的时候，带--recursive参数

  - 一直到make完都没有问题就可以

- 因为我安在了服务器上，而这个代码需要有交互界面，也就是会有GUI，所以安装了Xmanager

  - 安装了Xmanager后，也是使用XShell运行
    - 在Xshell：对应的shell-->属性-->隧道-->X11转移，选择上Xmanager(M)，点击“确定”
    - 然后记得，把打开的Xshell窗口全部关闭，再重新打开

- 下面开始运行code

  - 

  - ```
    cd developability-of-heightfields
    matlab
    ```

    - 这时候会通过出现matlab的GUI界面

  - 下面这几步在matlab的command windows中输入命令

    - ```
      addpath(genpath(path/to/developability-of-heightfields))
      ```

      - 这个地址是developability-of-heightfields的文件夹路径
      - 每次通过Xmanager打开GUI都要运行一次这个代码，添加路径

    - 如果是第一次运行developability-of-heightfields的代码，需要运行setup_mex。再运行就不用这步了

      - cd命令进入developability-of-heightfields/mex

      - 然后运行：

        - ```
          setup_mex

      - 等待运行完就可以

    - 走完上面这些，接下来Use

      - ```
        gui_developables('data/bunny.obj')
        ```

        - 这时候会出现一个GUI界面，具体上面的参数这里不介绍，第一次运行，可以直接先点击“Run”测试

        - 如果点击“Run”出现

          - ```
            glnxa64/libstdc++.so.6: version `GLIBCXX_3.4.26' not found这个问题
            ```

            - 我的处理方案

              - 先进入到matlabroot/sys/os/glnxa64，这里matlabroot是Matlab的安装地址

                - 将 libstdc++.so.6重命名为libstdc++.so.6.old 

              - 然后，将系统中的libstdc++.so.6链接到这里

                - ```
                  cd matlabroot/sys/os/glnxa64
                  然后运行：
                  ln -s /usr/lib32/libstdc++.so.6.0.28 libstdc++.so.6
                  ```

                  - 需要注意的一点，可以看看自己的libstdc++.so.6在哪个文件夹中，我的是在/usr/lib32这个文件夹中，也有可能在/usr/lib64这个文件夹中，只要在哪个文件夹中就链接哪个问价夹，然后文件夹内libstdc++.so.6.X这里自己文件夹内是哪个就链接哪个

          - 然后再重新运行

            - ```
              服务器上输入：matlab
              然后在新打开的matlab的GUI
              	addpath(genpath(path/to/developability-of-heightfields))
              	gui_developables('data/bunny.obj')
              	在界面点击"Run"
              ```

              - finish

        - 如果这里还不好，还是上面这个报错，我有运行过一次

          - ```
            sudo apt-get upgrade libstdc++6
            ```

            - 不知道这个是否有影响
