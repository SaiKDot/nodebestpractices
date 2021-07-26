[✔]: ../../assets/images/checkbox-small-blue.png

# 通用的Node.js Docker最佳实践

此通用Docker指南部分包含所有编程语言中标准化的最佳实践，并没有针对Node.js的特殊解释

## ![✔] 使用命令COPY优于ADD

**TL;DR:** COPY更安全，因为它只复制本地文件，而ADD支持更高级的获取，比如从远程站点下载二进制文件

## ![✔] 避免更新基础OS

**TL;DR:** 在构建期间更新本地二进制文件（例如apt get update）会在每次运行时创建不一致的映像，并且还需要提升权限。取而代之，使用经常更新的基础镜像

## ![✔] 使用标签对镜像分类

**TL;DR:** 为每个镜像提供元数据（metadata）可能有助于Ops专业人员充分处理它。例如，包括维护人员姓名、构建日期和其他信息，当有人需要对映像进行推理时，这些信息可能会被证明是有用的

## ![✔] 使用非特权容器

**TL;DR:** 特权容器具有与主机上的根用户相同的权限和功能。这是很少需要的，作为一个经验法则，应该使用在官方Node镜像中创建的'node'用户

## ![✔] 检查并验证最终结果

**TL;DR:** 有时很容易忽略构建过程中的副作用，如泄露的秘密或不必要的文件。使用[Dive](https://github.com/wagoodman/dive)等工具检查生成的镜像可以很容易地帮助识别此类问题

## ![✔] 执行完整性检查

**TL;DR:** 在拉取基本镜像或最终镜像时，网络可能会被误导并重定向到下载恶意镜像。除非对内容进行签名和验证，否则标准Docker协议中没有任何内容可以防止这种情况。[Docker Notary](https://docs.docker.com/notary/getting_started/)是一个可以执行此类检查的工具