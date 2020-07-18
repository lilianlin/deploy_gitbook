# 编写 Gitbook
无需本地安装 Gitbook, 按照 Gitbook 的要求编写 markdown 文本，提交到 Github 即可。

## Gitbook 结构
典型的 Gitbook 目录结构为：
```
docs
|__book.json (Optional)
|__README.md (Must)
|__SUMMARY.md (Must)
|__chapter-1
|  |__README.md
|  |__xxx.md
|__chapter-2
|  |__README.md
|  |__yyy.md
|__chapter-3
   |__README-md
   |__zzz.md
```

### book.json
Gitbook build时的配置文件，可缺省。

### README
一般为整个 Gitbook 的概述。

### SUMMARY
SUMMARY 为 Gitbook 的导航。通过 SUMMARY 将所有文件连接起来。

```markdown
# Context

* [Introduction](README.md)
* [Chap1](chapter-1/README.md)
    * [xxx](chapter-1/xxx.md)
* [Chap2](chapter-2/README.md)
    * [yyy](chapter-2/yyy.md)
* [Chap3](chapter-3/README.md)
    * [zzz](chapter-3/zzz.md)
```
