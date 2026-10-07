# CloudLeak Synthetic Detection Test

本仓库只用于测试 CloudLeak 对 GitHub 公开内容的采集与凭据检测。

## 安全声明

所有凭据样本均在本地随机生成，从未由任何云厂商或数据库签发，
不对应真实账号，不可用于登录或访问资源。样本旁均有明确的虚构声明。
所有主机名使用保留的 `.invalid` 域名。这里没有主项目代码、
生产配置、数据库备份、个人访问令牌，也没有可以启动的应用。

不要尝试使用这些样本调用真实云服务；不得用真实凭据替换它们。
本仓库保持为独立测试资产，不要导入任何现有项目文件。

## 测试内容

| 文件 | 测试项 |
| --- | --- |
| `.env` | AWS AK/SK 形状、MySQL 密码形状 |
| `config/aliyun/.env` | 阿里云 AK/SK 形状 |
| `config/tencent/.env` | 腾讯云 SecretId/SecretKey 形状 |
| `config/huawei/.env` | 华为云 AK/SK 形状 |
| `config/normal.env` | 环境变量引用与普通配置，预期无告警 |

共 9 个虚构凭据值。离线规则扫描产生 10 个命中：
同一个 MySQL 密码分别命中环境变量规则和配置密码规则，
因此 10 个命中不代表 10 个独立凭据。

## 结果边界

`expected-results.json` 记录现有生产检测引擎的离线基线，
不代表 GitHub 实际采集、告警通知、凭据有效性验证或分钟级延迟验收通过。
实际入库数量可能受去重、解析单元和采集方式影响。

公开发布后，将仓库 `Mrlujinyu/cloudleak-synthetic-test`
登记为 CloudLeak 的 repo 资产，再验证采集任务、原始证据、检测记录和来源链接。
GitHub 代码搜索需要等待索引；公开事件也可能延迟，不应提前声明验收成功。
