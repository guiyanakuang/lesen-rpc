lesen is a cross-language RPC framework

目录
1 简介

2 架构

3 使用指南

4 发展方向

1简介
> LesenRPC是一款基于netty和protobuffer的高性能RPC框架。LesenRPC 采用三层架构：传输层 协议层 应用层,
> 传输层:基于netty,充分利用netty提供异步的、事件驱动的功能,保证服务端的高并发 高性能.
> 协议层:基于protobufer,保证多语言无缝调用.
> 应用层:参考spring架构,采用工厂模式和观察者模式,对开发者既能透明化调用,也可以轻松的扩展,介入系统的任何流程.


2 架构

> Business code
> applacation(beanfactory+observer)
> procotols(protobuffer)
> Transport(netty)

3 使用指南
> 一 从这里获取源码: http://lesen-rpc.googlecode.com/svn/trunk/

> 二 服务端
  1. 制定要导出的接口,并将你的接口打包提供给客户端，如:
> > interface TestServiceItf {
> > > void add(int a,int b);
> > > }

> 2 提供一个服务端实现

> 3 创建RPCService app = new RPCService(1082);
> 4 导出你的服务app.exportService("test", new TestService());

> 5 调用RPCService.run()
参见: com.lesen.rpc.example.ServiceTest

package com.lesen.rpc.example;
> import com.lesen.rpc.common.export.TestService;
> import com.lesen.rpc.service.RPCService;

> public class ServiceTest {

> public static void main(String[.md](.md) args) throws Exception {
> > RPCService app = new RPCService(1082);
> > app.exportService("test", new TestService());
> > app.run();

> }
> }

三 客户端

> 参见:com.lesen.rpc.example.ClientTest

> package com.lesen.rpc.example;
> > import com.lesen.rpc.client.RPCClient;
> > import com.lesen.rpc.common.export.Service;


> public class ClientTest {

> public static void main(String[.md](.md) args) {
> > String serverName = "test";
> > String rpcUri = "rpc://127.0.0.1:1082";
> > RPCClient client = new RPCClient(rpcUri);
> > client.registDecodeEncode(new PersonDecodeEncode());
> > client.connectService();


> Service service = client.getRemoteService(serverName, Service.class);
> System.out.println(service.test("12"));
> client.close();
> }
> }




4 发展方向
1、支持多语言
2、针对移动设备优化客户端