我是光年实验室高级招聘经理。
我在github上访问了你的开源项目，你的代码超赞。你最近有没有在看工作机会，我们在招软件开发工程师，拉钩和BOSS等招聘网站也发布了相关岗位，有公司和职位的详细信息。
我们公司在杭州，业务主要做流量增长，是很多大型互联网公司的流量顾问。公司弹性工作制，福利齐全，发展潜力大，良好的办公环境和学习氛围。
公司官网是http://www.gnlab.com,公司地址是杭州市西湖区古墩路紫金广场B座，若你感兴趣，欢迎与我联系，
电话是0571-88839161，手机号：18668131388，微信号：echo 'bGhsaGxoMTEyNAo='|base64 -D ,静待佳音。如有打扰，还请见谅，祝生活愉快工作顺利。

# YuniKorn Scheduler for Kubernetes (yunikorn-k8shim)

YuniKorn scheduler shim for kubernetes is a customized k8s scheduler, it can be deployed in a K8s cluster and work as the scheduler.
This project contains the k8s shim layer code for k8s, it depends on `yunikorn-core` which encapsulates all the actual scheduling logic.
By default, it handles all pods scheduling if pod's spec has field `schedulerName: yunikorn`.

For detailed information on how to build the overall scheduler please see the [build document](https://github.com/cloudera/yunikorn-core/blob/master/docs/developer-guide.md) in the `yunikorn-core`.

## K8s-shim component build
This component build should only be used for development builds.
Prerequisites and build environment setup is described in the above mentioned build document.

### Build binary
The simplest way to get a local binary that can be run on a local Kubernetes environment is: 
```
make build
```
This command will build a binary `k8s_yunikorn_scheduler` under `_output/bin` dir. This binary is executable on local environment, as long as `kubectl` is properly configured.
Run `./k8s_yunikorn_scheduler -help` to see all options.

**Note**: it may take few minutes to run this command for the first time, because it needs to download all dependencies.

### Build run
If the local kubernetes environment is up and running you can build and run the binary via: 
```
make run
```
This will build the code, and run the scheduler with verbose logging. 
It will set the configuration for the scheduler to the provided default configuration `queues.yaml` and uses the current setup for kubernetes.

### Build and run tests
Unit tests for the shim only can be run via:
```
make test
```
Any changes made to the shim code should not cause any existing tests to fail.

### Build image steps
Build docker image can be triggered by running following command.

```
make image
```

You can set `TAG` and `VERSION` in the commandline to build docker image with a specified version and tag. For example,
```
make image TAG=yunikorn/yunikorn-scheduler-k8s VERSION=latest
```
This command will build a binary executable with version `latest` and the docker image tag is `yunikorn/yunikorn-scheduler-k8s:latest`.

You can run following command to retrieve the meta info for a docker image build, such as component revisions, date of the build, etc.

```
docker inspect --format='{{.Config.Labels}}' yunikorn/yunikorn-scheduler-k8s:latest
```

## Design documents
All design documents are located in a central location per component. The core component design documents also contains the design documents for cross component designs.
[List of design documents](docs/design/design-index.md) for the k8s-shim.

## How do I contribute code?

See how to contribute code in [this guide](docs/how-to-contribute.md).

