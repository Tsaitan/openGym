# 本地部署配置

此目录提供固定为 openGym 1.4.1 的官方 ARM64/AMD64 镜像配置，默认中文、仅本机访问，首个注册账户成为管理员。

从仓库根目录执行：

```bash
cd deploy/local
cp .env.example .env
mkdir -p data coach-auth
chmod 700 data coach-auth
docker compose up -d --wait --wait-timeout 90
```

打开 [http://localhost:8080](http://localhost:8080)，创建个人档案并完成通行密钥注册。

```bash
docker compose ps
docker compose logs --tail 100
curl -fsS http://localhost:8080/api/health
docker compose down
```

数据保存到本目录的 `data/`，认证缓存保存到 `coach-auth/`，均已排除在 Git 之外。AI Coach 需要管理员另行配置模型提供商。

本配置运行官方预构建镜像，不会自动使用本地修改后的源码。修改源码后，应使用仓库根目录的原有 `docker-compose.yml` 构建，并另行配置开发实例。

当前 Mac 的实例已部署在 `/Users/caixintan/Documents/ChatGPT/openGym`，继续在该目录管理现有实例即可。本目录是可复用的配置副本；不要在已有实例运行时再启动相同名称和端口的实例。新位置的 `data/` 是独立目录，迁移现有实例时需先停止并备份，再复制完整数据目录与 `.env`。

项目方案及本机部署记录见 [`docs/project`](../../docs/project)。
