Run Postgres in docker

```shell
docker run --name pg -p 5432:5432 -e POSTGRES_PASSWORD=postgres -d postgres:13.2
```

Setup database and user

```sql
create database ct_dev;
create user ct with encrypted password 'ct';
grant all privileges on database ct_dev to ct;
```

index 是有序的

[index types](https://www.postgresql.org/docs/current/indexes-types.html): B-tree, Hash, GiST, SP-GiST, GIN, BRIN

------

### [Postgres Indexes](https://devcenter.heroku.com/articles/postgresql-indexes)

#### Why is my query not using index?

Postgres planner 做了这个决定，并且大多数时候是正确的:

`select * from foo where bar = 1`

对于 bar = 2 可能行数要多很多，sequential scan 可能比 index scan 要快。

#### Partial Indexes

```sql
CREATE INDEX articles_flagged_created_at_index ON articles(created_at) WHERE flagged IS TRUE;
```

只是在 flagged IS TRUE 上做 index。

#### Expression Indexes

```sql
CREATE INDEX users_lower_email ON users(lower(email));
```

列上面做 expression 或者 function 之后建 index。

#### Unique Indexes

PRO: data integrity and performance

little distinction between unique indexes and unique constraints: unique indexes lower level, since partial indexes and expression indexes cannot be created as unique constraints.

#### Multi-column Indexes

same order: 比如有个 index on (a, b), `where a = x and b = y` 和 `where a = x` 都会用 index，但 `where b = y` 不会使用index。

#### B-Trees and sorting

B-Tree index entries 默认升序。

```sql
CREATE INDEX articles_published_at_index ON articles(published_at DESC NULLS LAST);
```

published_at 在没有发布时候是 null，NULLS LAST 能保证剩下的在最后。

#### 管理 indexes

用了 index 之后还是需要到 disk 取数据，或者 check visibility，所以都是要走 disk IO 的。

An index must be selective enough to reduce the number of disk lookups for it to be worth it.

create index 时候 lock the table against writes, 可以考虑 `create index concurrently`

`reindex` 也会 write lock，可以用另外一个名字 create index concurrently，drop 旧的，重命名到旧的。

------

[PG index 介绍](https://www.mengqingzhong.com/2020/10/01/postgresql-index-linnks/)

------

[Postgres performance](https://devcenter.heroku.com/categories/postgres-performance)

8k page

没有 index 时候 sequential scan



默认的 `create index` 创建的是 B-tree index

多列index 必须顺序一样才能起作用

MySQL index types

- const/eq_ref
- ref/range
- index
- ALL



[Postgres operator](https://github.com/CrunchyData/postgres-operator)

[zheap](https://cybertec-postgresql.github.io/zheap/)

[advanced indexing](https://www.slideshare.net/hansjurgenschonig/postgresql-advanced-indexing)

[postgres-showcase](https://github.com/cybertec-postgresql/postgres-showcase)

[digoal blog](https://github.com/digoal/blog)



[PG email 类型](https://github.com/digoal/blog/blob/master/202001/20200106_02.md) to Django
