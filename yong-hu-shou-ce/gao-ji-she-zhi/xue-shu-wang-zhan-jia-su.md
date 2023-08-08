# 学术网站加速

## 声明

在您使用我们的学术资源加速服务之前，请您仔细阅读以下声明：

1. **服务目标**：此服务旨在解决中国国内网络环境以及跨境网络速度慢的问题，为用户提供学术资源的加速访问。
2. **无稳定性保证**：请注意，我们并不能保证这项服务的稳定性。尽管我们一直在努力提供最佳服务，但由于网络环境和其他无法控制的因素，服务可能会出现间歇性中断或者速度变慢的情况。
3. **用户违规使用的应对**：我们严格禁止任何形式的违规使用。一旦发现违规行为，我们将追究相关责任，并可能会立即停止为该用户提供服务。

## 加速网站

* github
* githubusercontent.com
* githubassets.com
* huggingface

## 使用方法

在终端中执行以下命令后，使用git clone、wget等请求时将具有学术加速能力。

### 北京1区工作空间

```
export http_proxy=http://172.16.254.2:10800 && export https_proxy=http://172.16.254.2:10800
```

### 北京2区工作空间

```
export http_proxy=http://172.22.72.5:10800 && export https_proxy=http://172.22.72.5:10800
```

### 北京3区工作空间

```
export http_proxy=http://172.22.52.128:10800 && export https_proxy=http://172.22.52.128:10800
```

### 华东1区工作空间

```
export http_proxy=http://172.22.96.4:10800 && export https_proxy=http://172.22.96.4:10800
```

## 关闭加速

```
unset http_proxy && unset https_proxy
```
