```sql
create table event (
  id serial primary key,  
  created_at timestamp default current_timestamp,
  is_deleted boolean default false,
  parent_id integer default 0,
  related_table varchar(128) not null,
  related_id integer not null,
  sender_id integer not null,
  receiver_level varchar(128) not null,
  receiver_id integer not null,
  body jsonb default '{}'
);

```


[1]: http://www.jianshu.com/p/f4d7827821f1
[2]: https://www.jianshu.com/p/6bf8166b291c
[3]: http://blog.jobbole.com/42256/
[4]: https://segmentfault.com/q/1010000000672529
[5]: http://www.woshipm.com/pd/28763.html
[6]: https://github.com/dongjun111111/blog/issues/18
