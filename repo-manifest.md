# repo manifest

本文主要介绍'repo manifest'命令的使用，如果只对结论感兴趣，请直接跳转到 \[第4节 总结\]。

> 说明：  
> 1. 本文基于repo v1.12.37和repo launcher 1.23  
> 2. 文中manifest文件有时也称为清单文件  
> 3. 文中对40个字符的commit id进行截断处理，例如将"221a1acee8047ae65c2d5980e3a7c5f73362c59d"截断为8个字符的"221a1ace"

### 1. manifest文件之痛

有没有遇到过这样的场景：

例如，想冻结某个时间点调试好的代码，将其manifest保存起来，以备将来使用。

例如，像安卓这样的repo库，每天甚至每小时都有代码不断被check in, 因此代码推进很快，有时为了确保在同一基线的代码上工作，需要导出并共享manifest文件。

好吧，有人可能会说，直接保存'.repo/manifest.xml'文件不就可以了吗？

可惜，答案是否定的。为什么？打开'.repo/manifest.xml'文件看看就知道了。

以android官方的aosp库为例，先下载manifest清单库：

```text
$ repo init -u https://android.googlesource.com/platform/manifest
```

先看看'.repo/manifest.xml'文件的内容：

```text
$ cat .repo/manifest.xml
...
  <project path="art" name="platform/art" groups="pdk" />
  <project path="bionic" name="platform/bionic" groups="pdk" />
  <project path="bootable/recovery" name="platform/bootable/recovery" groups="pdk" />
  <project path="compatibility/cdd" name="platform/compatibility/cdd" groups="pdk" />
  <project path="cts" name="platform/cts" groups="cts,pdk-cw-fs,pdk-fs" />
```

每个project节点都指定了path, name和groups，但是并没有指定版本，此时默认为master分支引用，同步时会获取master分支。所以这就是为什么每次运行完'repo sync'命令后拿到的都是master分支最新的代码。

再次问一下，直接保存'.repo/manifest.xml'文件能确保代码处于某个冻结的状态吗？

> 又如这篇文章：[https://blog.csdn.net/dddddttttt/article/details/80792762](https://blog.csdn.net/dddddttttt/article/details/80792762)
>
> 作者记录了使用Qemu运行ARMv8的OP-TEE代码，在文章的最后说记录下他当时Arm v8的版本commit id, 避免万一以后github更新导致无法运行。&lt;/br&gt; 因此保存了'.repo/manifest.xml'文件，但他保存的清单文件中很多project并没有指定版本，过了一段时间后，如果再使用这个清单文件同步代码，对于没有指定revision的project，会取master分支的最新代码，因此同步后的代码就变了，不再是他保存清单文件时的状态。

为了确保repo库的代码冻结在某个版本，需要manifest文件中所包含的每一个project节点都有一个确定的版本。只有每个project节点的版本都确定了，最终的代码才是确定的，也才能确保在另外一个时间点用这个manifest文件得到的是完全一样的代码。

那如何做呢？'repo manifest'命令可以做到。

### 2. 'repo manifest'命令详解

> 以下操作以OP-TEE库的manifest为例，选OP-TEE是因为其包含的project比较少，便于演示，千万不要以为只有Andrid才使用repo啊。&lt;/br&gt; OP-TEE库的地址：[https://github.com/op-tee](https://github.com/op-tee)

'repo manifest'命令很简单，主要是3个选项，具体信息请用'repo help manifest'或'repo manifest -h'查看。

> 好吧，我觉得很多人还是不会去看，这里贴一下简单的帮助信息：&lt;/br&gt;
>
> ```text
> $ repo manifest -h
> Usage: repo manifest [-o {-|NAME.xml} [-r]]
>
> Options:
>   -h, --help            show this help message and exit
>   -r, --revision-as-HEAD
>                         Save revisions as current HEAD
>   --suppress-upstream-revision
>                         If in -r mode, do not write the upstream field.  Only
>                         of use if the branch names for a sha1 manifest are
>                         sensitive.
>   -o -|NAME.xml, --output-file=-|NAME.xml
>                         File to save the manifest to
> ```

除了'-h'选项意外，'repo manifest'的主要操作有：

1. 不带任何选项

不带任何选项的'repo manifest'命令会在命令行输出当前使用的manifest信息，如：

```text
$ repo manifest
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
  <remote fetch="https://github.com" name="github"/>

  <default remote="github" revision="master"/>

  <project clone-depth="1" name="ARM-software/arm-trusted-firmware.git" path="arm-trusted-firmware" revision="refs/tags/v1.5-rc2"/>
  <project name="OP-TEE/build.git" path="build">
    <linkfile dest="build/Makefile" src="qemu_v8.mk"/>
    <linkfile dest="build/gdb" src="../toolchains/aarch64/bin/aarch64-linux-gnu-gdb"/>
  </project>
  <project name="OP-TEE/optee_client.git" path="optee_client"/>
  <project name="OP-TEE/optee_os.git" path="optee_os"/>
  <project name="OP-TEE/optee_test.git" path="optee_test"/>
  <project clone-depth="1" name="buildroot/buildroot.git" path="buildroot" revision="refs/tags/2018.08"/>
  <project name="linaro-swg/linux.git" path="linux" revision="221a1ace"/>
  <project name="linaro-swg/optee_benchmark.git" path="optee_benchmark"/>
  <project name="linaro-swg/optee_examples.git" path="optee_examples"/>
  <project name="linaro-swg/soc_term.git" path="soc_term" revision="5493a6e7"/>
  <project clone-depth="1" name="qemu/qemu.git" path="qemu" revision="refs/tags/v2.12.0"/>
  <project name="tianocore/edk2.git" path="edk2" revision="dd4cae4d"/>
</manifest>
```

> 注：这里的revision已经手动进行了截断处理，将"221a1acee8047ae65c2d5980e3a7c5f73362c59d"截断为8个字符的"221a1ace"，下同。

如果项目是由多个manifest组成，例如默认的manifest.xml和local\_manifest.xml，在输出中会将这些manifest信息合并到一起。

1. '-r'选项

'-r'选项解释说将各个项目的revision设置为其当前的HEAD指针。也就是说，其HEAD引用指向具体的提交。如下：

```text
$ repo manifest -r
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
  <remote fetch="https://github.com" name="github"/>

  <default remote="github" revision="master"/>

  <project clone-depth="1" name="ARM-software/arm-trusted-firmware.git" path="arm-trusted-firmware" revision="16b05e94" upstream="refs/tags/v1.5-rc2"/>
  <project name="OP-TEE/build.git" path="build" revision="0c76195e" upstream="master">
    <linkfile dest="build/Makefile" src="qemu_v8.mk"/>
    <linkfile dest="build/gdb" src="../toolchains/aarch64/bin/aarch64-linux-gnu-gdb"/>
  </project>
  <project name="OP-TEE/optee_client.git" path="optee_client" revision="c48bc3be" upstream="master"/>
  <project name="OP-TEE/optee_os.git" path="optee_os" revision="b31756b3" upstream="master"/>
  <project name="OP-TEE/optee_test.git" path="optee_test" revision="78aa0ffc" upstream="master"/>
  <project clone-depth="1" name="buildroot/buildroot.git" path="buildroot" revision="339d550e" upstream="refs/tags/2018.08"/>
  <project name="linaro-swg/linux.git" path="linux" revision="221a1ace"/>
  <project name="linaro-swg/optee_benchmark.git" path="optee_benchmark" revision="845a7835" upstream="master"/>
  <project name="linaro-swg/optee_examples.git" path="optee_examples" revision="552c9d08" upstream="master"/>
  <project name="linaro-swg/soc_term.git" path="soc_term" revision="5493a6e7"/>
  <project clone-depth="1" name="qemu/qemu.git" path="qemu" revision="4743c235" upstream="refs/tags/v2.12.0"/>
  <project name="tianocore/edk2.git" path="edk2" revision="dd4cae4d"/>
</manifest>
```

从命令输出的结果可以看到，这里多个project\(包括'build.git', 'optee\_client.git', 'optee\_os.git'和'optee\_test.git'等 \)的upstream都是"master"。 默认master分支会拉取master分支最新代码的，但由于这里指定了revision，所以即使是master分支，也只取revision为commit id的代码。

1. '--suppress-upstream-revision'选项

选项的说明中提到，在'-r'模式下，使用这个选项不往manifest文件中写入upstream属性。

因此这个选项只有在`-r`选项打开时才有用。在使用`-r`选项时，如果原来manifest中的project版本是指向某个节点的引用，如：

```text
<project clone-depth="1" name="qemu/qemu.git" path="qemu" revision="refs/tags/v2.12.0"/>
```

此时输出的manifest会包含一个upstream属性：

```text
<project clone-depth="1" name="qemu/qemu.git" path="qemu" revision="4743c235" upstream="refs/tags/v2.12.0"/>
```

这里的'revision'指向具体的commit id，而upstream指向原来的revision引用，即`refs/tags/v2.12.0`。

如果'-r'和'--suppress-upstream-revision'选项同时使用，输出的project节点中不再包含upstream属性，如：

```text
$ repo manifest -r --suppress-upstream-revision
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
  <remote fetch="https://github.com" name="github"/>

  <default remote="github" revision="master"/>

  <project clone-depth="1" name="ARM-software/arm-trusted-firmware.git" path="arm-trusted-firmware" revision="16b05e94"/>
  <project name="OP-TEE/build.git" path="build" revision="0c76195e">
    <linkfile dest="build/Makefile" src="qemu_v8.mk"/>
    <linkfile dest="build/gdb" src="../toolchains/aarch64/bin/aarch64-linux-gnu-gdb"/>
  </project>
  <project name="OP-TEE/optee_client.git" path="optee_client" revision="c48bc3be"/>
  <project name="OP-TEE/optee_os.git" path="optee_os" revision="b31756b3"/>
  <project name="OP-TEE/optee_test.git" path="optee_test" revision="78aa0ffc"/>
  <project clone-depth="1" name="buildroot/buildroot.git" path="buildroot" revision="339d550e"/>
  <project name="linaro-swg/linux.git" path="linux" revision="221a1ace"/>
  <project name="linaro-swg/optee_benchmark.git" path="optee_benchmark" revision="845a7835"/>
  <project name="linaro-swg/optee_examples.git" path="optee_examples" revision="552c9d08"/>
  <project name="linaro-swg/soc_term.git" path="soc_term" revision="5493a6e7"/>
  <project clone-depth="1" name="qemu/qemu.git" path="qemu" revision="4743c235"/>
  <project name="tianocore/edk2.git" path="edk2" revision="dd4cae4d"/>
</manifest>
```

1. '-o -\|NAME.xml'选项

这里'-o'选项可以带参数'-'或具体的manifest文件名。

不带'-o'或'-o'选项的参数为'-'时，直接在标准输出上显示manifest信息。如果设置'-o name.xml'，则会将manifest信息输出到name.xml文件中。如：

```text
$ repo manifest -r --suppress-upstream-revision -o name.xml
Saved manifest to name.xml
$ cat name.xml 
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
  <remote fetch="https://github.com" name="github"/>

  <default remote="github" revision="master"/>

  <project clone-depth="1" name="ARM-software/arm-trusted-firmware.git" path="arm-trusted-firmware" revision="16b05e94"/>
  <project name="OP-TEE/build.git" path="build" revision="0c76195e">
    <linkfile dest="build/Makefile" src="qemu_v8.mk"/>
    <linkfile dest="build/gdb" src="../toolchains/aarch64/bin/aarch64-linux-gnu-gdb"/>
  </project>
  <project name="OP-TEE/optee_client.git" path="optee_client" revision="c48bc3be"/>
  <project name="OP-TEE/optee_os.git" path="optee_os" revision="b31756b3"/>
  <project name="OP-TEE/optee_test.git" path="optee_test" revision="78aa0ffc"/>
  <project clone-depth="1" name="buildroot/buildroot.git" path="buildroot" revision="339d550e"/>
  <project name="linaro-swg/linux.git" path="linux" revision="221a1ace"/>
  <project name="linaro-swg/optee_benchmark.git" path="optee_benchmark" revision="845a7835"/>
  <project name="linaro-swg/optee_examples.git" path="optee_examples" revision="552c9d08"/>
  <project name="linaro-swg/soc_term.git" path="soc_term" revision="5493a6e7"/>
  <project clone-depth="1" name="qemu/qemu.git" path="qemu" revision="4743c235"/>
  <project name="tianocore/edk2.git" path="edk2" revision="dd4cae4d"/>
</manifest>
```

通过带有'-r'选项的'repo manifest'命令，输出manifest中每一个project节点都有一个指向具体commit id的revision属性，有了这个revision, 整个代码的状态就能确定下来了。

问题来了，得到这样的一个清单文件后该如何使用呢？

### 3. 清单文件的使用

通过'repo manifest'操作导出manifest文件。如果需要包含每一个git库当前的版本信息，则需要使用'-r'选项。

拿到导出的清单文件name.xml后，将文件放到'.repo/manifests/'目录下，调用带'-m'选项的repo init'命令，如：

```text
$ cp name.xml .repo/manifests/
$ repo init -m name.xml
```

'repo init'之后，就是通过'repo sync'同步代码了。

或许有人要问为什么要放到'.repo/manifest/'目录下，放到其他目录或当前目录不行吗？

因为对于'-m'选项，代码只在'.repo/manifest/'目录下去查找'-m'选项指定的manifest文件。

最后让我来告诉你命令'repo init -m name.xml'到底发生了什么吧。

首先，repo获取manifest库\('.repo/manifests'\)的更新。 然后，将'.repo/manifests/default.xml'文件链接到'.repo/manifest.xml'。

由于使用了'-m'选项，所以会将'-m'指定的清单文件'.repo/manifest/name.xml'链接到'.repo/manifest.xml'，而不再使用默认的'.repo/manifests/default.xml'。

> 理论上，如果你拿到一个清单文件name.xml，通过命令'ln -s name.xml .repo/manifest.xml'直接将其连接到'.repo/manifest.xml'也是可以的。 但实际操作上，在接下来的'repo sync'时会报找不到'.repo/manifest.xml'文件的错误。 所以还是不行。

### 4. 总结

#### 导出manifest文件

1\). 导出当前使用清单

导出当前使用的manifest清单到name.xml文件:

```text
$ repo manifest -o name.xml
```

2\). 导出带版本信息清单

导出包含版本信息的manfiest清单到name.xml文件：

```text
$ repo manifest -r -o name.xml
```

> 如果本地所用的manifest由多个文件组成，'repo manifest'命令会将这几个文件的内容一起输出。

#### 使用导出的manifest文件

使用导出的name.xml清单进行初始化，并同步代码：

```text
$ cp name.xml .repo/manifests
$ repo init -m name.xml
$ repo sync
```

### 5. 最后更新: 2020/01/02

