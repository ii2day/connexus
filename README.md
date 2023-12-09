# connexus
tcp udp connection pool management


```go
cfg := PoolConfig{
	Cap: 30,
	MaxIdleCap:35,
	Factory: func() (net.Conn, error) { return net.Dial("tcp", "localhost:7777") }
}
pool := NewConnexPool(cfg)

conn,err := pool.Get()

// do something

// 链接会重新放回池中
conn.Close()

// 若希望关闭底层链接
conn.MarkUnusable()
// 再次调用，后底层链接将会关闭，链接不会放入池中
conn.Close()

//关闭连接池，池中的链接将会随之关闭
pool.Close()

```