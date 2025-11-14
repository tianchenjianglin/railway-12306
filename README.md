# railway-12306

railway-12306 是一个仿照 12306 网站设计的铁路购票系统，旨在提供一个高并发、分布式架构下的购票系统参考实现。该项目基于 Spring Cloud 和 Alibaba 微服务架构，结合了多种分布式组件，如 RocketMQ、Redis、ShardingSphere、Feign、Sentinel 等，实现了购票、支付、订单管理、用户管理等核心功能。

## 技术栈

- **Spring Boot / Spring Cloud / Spring Cloud Alibaba**
- **MyBatis Plus / ShardingSphere**（数据库分库分表）
- **Redis / Redisson**（缓存、分布式锁）
- **RocketMQ**（异步消息队列）
- **Feign / OpenFeign**（服务间通信）
- **Sentinel / Nacos**（服务治理与配置中心）
- **XXL-JOB**（定时任务）
- **Hippo4j**（动态线程池）
- **Canal / RocketMQ**（数据同步）
- **Vue.js**（前端页面）

## 功能模块

### 用户服务（User Service）
- 用户注册、登录、注销
- 用户信息管理
- 乘车人信息管理
- 用户注销与复用机制
- 基于 Redis 的缓存穿透防护（BloomFilter）

### 车票服务（Ticket Service）
- 车次信息管理
- 车站、区间查询
- 车票库存管理
- 座位选择与锁定机制
- 车票购买、退票、改签
- 基于 Token Bucket 的车票可用性控制

### 订单服务（Order Service）
- 订单创建、查询、取消、关闭
- 订单状态管理
- 基于 RocketMQ 的订单延迟关闭机制
- 订单状态反转机制

### 支付服务（Pay Service）
- 支付接口集成（如支付宝）
- 支付回调处理
- 退款机制
- 支付结果异步通知

### 聚合服务（Aggregation Service）
- 统一服务聚合入口
- 整合用户、车票、订单、支付等服务
- 提供统一的接口调用链路

### 网关服务（Gateway Service）
- 统一 API 入口
- Token 校验
- 路由控制与权限拦截

## 特色功能

- **高并发场景优化**：通过 Redis 缓存、分布式锁、Token Bucket、线程池等手段提升系统吞吐量。
- **分布式 ID 生成**：使用 Snowflake 改进算法生成全局唯一订单 ID、支付 ID。
- **幂等性控制**：通过自定义注解 + Redis 实现接口幂等性，防止重复提交。
- **服务链路追踪**：集成日志打印与链路追踪，便于调试与监控。
- **数据同步机制**：通过 Canal + RocketMQ 实现数据库 Binlog 同步至缓存，保证数据一致性。
- **任务调度**：使用 XXL-JOB 实现缓存预热、数据同步等定时任务。

## 项目结构

- **console-vue**：前端 Vue 项目，提供用户操作界面。
- **frameworks/**：通用组件模块，包括缓存、日志、线程池、幂等、异常处理等。
- **services/**：微服务模块，包含用户、车票、订单、支付、聚合、网关等服务。
- **tests/**：测试模块，包含单元测试与集成测试。

## 快速启动

### 前端启动

```bash
# 进入前端目录
cd console-vue

# 安装依赖
yarn install

# 启动开发环境
yarn serve

# 构建生产环境
yarn build
```

### 后端启动

1. **依赖服务启动**：确保 MySQL、Redis、RocketMQ、Nacos、Sentinel、XXL-JOB 等中间件已启动。
2. **导入数据库**：根据 `resources/db/` 中的 SQL 文件初始化数据库。
3. **启动微服务**：依次启动 `user-service`, `ticket-service`, `order-service`, `pay-service`, `aggregation-service`, `gateway-service`。
4. **访问接口文档**：通过 Swagger 或 Knife4j 查看接口文档。

## 开发者指南

- **代码风格**：使用 Lombok、Slf4j、Spring Boot Starter 等现代化开发工具。
- **异常处理**：统一异常处理机制，支持自定义错误码与异常封装。
- **日志打印**：通过 AOP 实现接口日志打印，便于追踪请求链路。
- **配置中心**：使用 Nacos 管理各服务配置，支持动态刷新。
- **服务注册与发现**：基于 Nacos 实现服务注册与发现。

## 开源协议

本项目采用 **MIT License** 开源协议，欢迎贡献代码与提出建议。

## 联系方式

- 作者：Bushituo
- Gitee 地址：[railway-12306](https://gitee.com/bu-shituo/railway-12306)

---

railway-12306 是一个完整的铁路购票系统参考实现，适用于学习微服务架构、高并发系统设计、分布式事务等场景。欢迎 Star、Fork 与贡献代码！