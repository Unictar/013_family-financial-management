# 家庭财务管理系统

---

## 项目简介

家庭财务管理系统（Family Financial Management System）是一款面向家庭的轻量级 Web 财务管理工具，帮助家庭成员便捷地记录、统计和管理日常收支，实现财务数据可视化，为家庭财务决策提供数据支持。

### 核心功能

- **用户认证**：注册/登录/退出，MD5 加密，Session + Cookie 双重会话保持
- **收支管理**：收入与支出快速录入、分页查询、多条件筛选，月度预算 200 元超额预警
- **资产管理**：活期账户、负债跟踪、投资管理、理财产品推荐（R1-R5 风险等级）、支付方式管理
- **数据可视化**：首页仪表盘（排行榜 + ECharts 饼图/柱状图/折线图），收支趋势分析
- **多用户协同**：基于家庭（House）的数据隔离，三级角色权限（系统管理员/家庭管理员/普通成员）
- **系统管理**：用户管理、角色管理、权限树分配、动态菜单

### 技术栈

| 层级 | 技术 |
|------|------|
| 后端框架 | Spring Boot 2.4.5 |
| 数据持久化 | MyBatis + MyBatis-Spring-Boot-Starter 2.1.4 |
| 数据库连接池 | Alibaba Druid 1.1.22 |
| 模板引擎 | Thymeleaf |
| 前端框架 | Layui + XAdmin 主题 |
| 图表库 | ECharts 5 |
| 数据库 | MySQL |
| 构建工具 | Maven |
| JDK | 1.8 |

---

## 环境依赖

- **JDK**：1.8+
- **Maven**：3.6+
- **MySQL**：5.7+（推荐 8.0）
- **IDE**：IntelliJ IDEA（推荐）

---

## 快速开始

### 1. 克隆项目

```bash
git clone https://github.com/Unictar/013_family-financial-management.git
cd 013_family-financial-management
```

### 2. 数据库初始化

登录 MySQL，创建数据库并导入建表脚本：

```sql
CREATE DATABASE IF NOT EXISTS ffms DEFAULT CHARACTER SET utf8mb4;
```

```bash
mysql -u root -p ffms < sql/ffms_schema_recommended.sql
```

### 3. 修改配置

编辑 `src/main/resources/application.yml`，修改数据库连接信息：

```yaml
spring:
  datasource:
    druid:
      url: jdbc:mysql://127.0.0.1:3306/ffms?characterEncoding=utf-8&serverTimezone=UTC&useSSL=false
      username: root
      password: 你的密码
```

### 4. 启动项目

```bash
mvn spring-boot:run
```

启动成功后，访问 **http://localhost:8081** 进入系统。

---

## 目录结构

```
013_family-financial-management/
├── sql/                                # 数据库脚本
│   └── ffms_schema_recommended.sql     # 建表 DDL + 初始数据
├── docs/                               # 项目文档
│   ├── 软件需求说明书.docx
│   └── 数据库设计说明书.docx
├── src/main/java/com/xust/ffms/
│   ├── FfmsApplication.java           # Spring Boot 启动类
│   ├── configs/                        # 配置类（CORS / Session / MD5 / 日志拦截器）
│   ├── controller/                     # 控制器层（REST API + 页面路由）
│   ├── service/                        # 服务接口
│   │   └── impl/                       # 服务实现
│   ├── dao/                            # MyBatis Mapper 接口
│   ├── entity/                         # 实体类
│   └── utils/                          # 工具类（分页 / 响应封装 / 日期处理）
├── src/main/resources/
│   ├── application.yml                 # 应用配置
│   ├── mappers/                        # MyBatis XML 映射文件
│   ├── templates/                      # Thymeleaf HTML 模板
│   └── static/                         # 静态资源（CSS / JS / 字体 / 图片）
├── pom.xml                             # Maven 项目配置
├── .gitignore
└── README.md
```

---

## 系统角色

| 角色 | 权限范围 |
|------|----------|
| 系统管理员 (roleid=1) | 管理所有用户、角色、权限，查看全部数据 |
| 家庭管理员 (roleid=2) | 管理本家庭成员和财务数据 |
| 普通成员 (roleid=3) | 记录个人收支，查看家庭统计数据 |

---

## 团队信息

- **项目名称**：家庭财务管理系统
- **团队名称**：013-基因重组
- **开发周期**：2026 年 3 月 21 日 — 2026 年 6 月 13 日

### 团队成员

| 姓名 | 学号 | 角色 | 职责 |
|------|------|------|------|
| 侯宇慧 | 231110373 | 产品经理/项目经理 | 统筹项目全流程、进度管理、团队协调 |
| 郑安娜 | 231110120 | 产品助理/需求专员 | 需求分析、文档编写、测试评审 |
| 蔡奕彤 | 231110118 | 后端工程师/技术负责人 | 系统架构、后端开发、技术选型 |
| 林洁珊 | 231110173 | UI设计师/前端工程师 | UI设计、前端开发、用户体验 |
| 刘佳妮 | 231110169 | 测试工程师 | 测试计划、用例设计、质量保障 |
