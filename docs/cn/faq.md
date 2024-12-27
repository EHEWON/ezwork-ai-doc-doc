# FAQ常见问题

---

> Q：如何停止服务？

A：要停止所有服务，可以运行：

```bash
docker stop ezwork-ai
```

> Q：如何查看日志？

A：要查看服务的日志，可以使用：

```bash
docker logs ezwork-ai
```

> Q：如何访问数据库？

A：你可以通过 MySQL 客户端连接到数据库，使用以下连接信息：

```bash
docker exec -it ezwork-ai mysql -uroot -pezwork ezwork
```