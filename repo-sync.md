# repo sync

说来有点丢人，我用了`repo`很长一段时间以后，只会也只用`repo init`和`repo sync`两个命令。这段时间差不多有两年吧，逃~

每次使用`repo init`都要上网搜索一下用法。因为感觉参数太多了啊，又是`-u`，`-b`，又是`-m`啥的，根本不知道是个嘛意思。如果你也是这样，哈哈，你并不孤单。

`repo sync`够简单，不用带参数也可以正常工作，所以倒也不需要上网去搜索用法。但唯一会的就是`-j`选项，为啥会用`-j`选项，因为平时在服务器上编译习惯用`make -j32`这样的指令了，而且也看到别人在网上贴过这个选项，所以也就只知道这个。

当然也可能因为支持客户，几乎不需要提交代码，所以也从来没想过要去用其它命令。

## 1. repo sync之痛

* 为了省空间，对方将代码打包发给你，但里面只包含了一个`.repo`目录，你收到代码后如何还原代码？别说没有这种情况啊，
* 同步中最烦人的就是代码有很多分支，但是你只想要你感兴趣的那个分支，结果你一同步代码，整个库都搬过来了~~就好像你去传达室取信件，结果传达室大爷给你一麻袋，说全部都在这里了，你自己拿吧……

### 情景1. 如何单独同步某个git库？

> 最近android项目中，内核组的同事说解决了几个关键问题，需要在本地代码中同步他们的更新，但你不想更新所有代码，因为android有小几百个git库，你不知道全部更新会不会惹出其它问题，所以想且只想更新linux代码。

### 情景2. 如何只将本地.repo目录的代码拿出来？

> 为了节省空间，合作伙伴将代码打包发给你，但里面只包含了一个`.repo`目录，你收到代码包后如何还原代码？

### 情景3. 如何只同步必要的数据？

> 同步的代码有很多功能特性分支，但是你只想下载感兴趣那个分支，但是通常一同步代码，所有库都会更新。就好像你去传达室取信件，结果传达室的大爷指给你一大麻袋，说信件全部都在这里了，你自己拿吧……

## 2. repo sync 帮助信息

```text
$ repo sync -h
Usage: repo sync [<project>...]

Options:
  -h, --help            show this help message and exit
  -f, --force-broken    obsolete option (to be deleted in the future)
  --fail-fast           stop syncing after first error is hit
  --force-sync          overwrite an existing git directory if it needs to
                        point to a different object directory. WARNING: this
                        may cause loss of data
  --force-remove-dirty  force remove projects with uncommitted modifications
                        if projects no longer exist in the manifest. WARNING:
                        this may cause loss of data
  -l, --local-only      only update working tree, don't fetch
  -n, --network-only    fetch only, don't update working tree
  -d, --detach          detach projects back to manifest revision
  -c, --current-branch  fetch only current branch from server
  -q, --quiet           be more quiet
  -j JOBS, --jobs=JOBS  projects to fetch simultaneously (default 1)
  -m NAME.xml, --manifest-name=NAME.xml
                        temporary manifest to use for this sync
  --no-clone-bundle     disable use of /clone.bundle on HTTP/HTTPS
  -u MANIFEST_SERVER_USERNAME, --manifest-server-username=MANIFEST_SERVER_USERNAME
                        username to authenticate with the manifest server
  -p MANIFEST_SERVER_PASSWORD, --manifest-server-password=MANIFEST_SERVER_PASSWORD
                        password to authenticate with the manifest server
  --fetch-submodules    fetch submodules from server
  --no-tags             don't fetch tags
  --optimized-fetch     only fetch projects fixed to sha1 if revision does not
                        exist locally
  --prune               delete refs that no longer exist on the remote
  -s, --smart-sync      smart sync using manifest from the latest known good
                        build
  -t SMART_TAG, --smart-tag=SMART_TAG
                        smart sync using manifest from a known tag

  repo Version options:
    --no-repo-verify    do not verify repo source code
```

## 最后更新: 2020/01/02

