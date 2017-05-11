
[Database](#database)

- Avoid using nullable fields in your DB. Put `not null` everywhere you can when
  defining a table. Assign a default blank value if submitting a field is not
  necessary:

  ```sql
  create table foo (
    ...
    comment text not null default '',
    count integer not null defult 0
  );
  ```

- Keep your database migrations in raw `*.sql` files. Wrap each migration into
  transaction explitly putting `begin;` and at the top of file and `commit;` at
  the bottom.

- Don't delete anything from your DB. Add `deleted` boolean flag that is false
  by default and put `AND NOT mytable.deleted` in `WHERE` or `JOIN` statements:

  ```sql
  select * from foo where not deleted;
  ```

  ```sql
  select *.f, *.b
  from foo f
  left join bar b on foo.bar_id = b.id and not b.deleted;
  ```

- For each table, add `created_at` that fixates creation time automatically:

  ```sql
  create table foo (
    ...
    created_at timestamp not null default current_timestamp;
  );
  ```
