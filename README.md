postgres worker adapter for buffalo
===================================

This package implements the `github.com/gobuffalo/buffalo/worker.Worker` interface using the [`https://github.com/jackc/pgx`](https://github.com/jackc/pgx) package

It allows postgres to be used for processing [buffalo's background tasks](https://gobuffalo.io/en/docs/workers).

## Setup

```go
import "github.com/mrhillsman/postgres-work-adapter"
import "github.com/jackc/pgx"

// ...

conn, err := pgx.Connect(context.Background(), os.Getenv("DATABASE_URL"))
if err != nil {
    log.Fatal(err)
}

buffalo.New(buffalo.Options{
  // ...
  Worker: pgsqlw.New(pgsqlw.Options{
    Connection: conn,
    Name: "myapp",
    MaxConcurrency: 25,
  }),
  // ...
})
```
