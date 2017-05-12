### [Database](#database)

- Avoid using nullable fields in your DB. Put `not null` everywhere you can when
  defining a table. Assign a default blank value if submitting a field is not
  necessary:

  ```sql
  create table foo (
    ...
    comment text not null default '',
    count integer not null default 0
  );
  ```

- Keep your database migrations in raw `*.sql` files. Wrap each migration into
  transaction explicitly putting `begin;` and at the top of file and `commit;`
  at the bottom:

  ```sql
  --
  -- A short comment about what this migration does.
  --
  begin;

  update foo set bar = 42 where id = 100500;

  alter table baz drop column test;

  commit;
  ```

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

- Once you've got any geographical data (locations, areas, routes), install
  PostGIS extension without inventing your own "smart" algorithms. They will let
  you down one Friday evening.

- Postgres is great for full-text searching. Try to deal with standard
  PostgreSQL capabilities before installing Elastic, Sphinx and related stuff.

- Avoid using ORMs. A small wrapper that parses `*.sql` files and creates plain
  functions would be enough.

- Don't use triggers to implement business logic. Such behaviour is quite
  implicit and difficult to maintain. And business rules changes all the time.

### [Code](#code)

- Don't align you code with spaces like it's shown below. Use one space only.

  ```python
  foo = {
    "short":              1,
    "a-bit-longer":       2,
    "very-very-long-one": 3,
  }
  ```
- Write unit tests for both server and UI sides immediately once you've started
  a new project.

- Classes are not data. Prefer plain data structures like lists and maps over
  classes. Usually, structures are fast and covers the most of requirements.

- Try to follow functional approach when develop a program. Avoid keeping state
  where it can be skipped. Separate IO from a code that does pure calculations.

### [Frontend](#frontend)

- Don't use vanilla Javascript. Use such modern technologies as ClojureScript,
  TypeScrip or Elm to develop without a pain in the ass. Consider JS as
  necessary evil needed under the hood to ship your application.

- Don't make SAPs (single page applications). Usually they work poorly, the
  layout leaks, you cannot open a link in a new window what is breaking W3C
  standards.

### [Architecture](#architecture)

- Don't make micro-services. Try to keep the whole codebase within. Run
  different domains of your application in separate threads as components.

- Queues might help a lot. Don't invent your own message queue facility. Use
  Rabbit, ZeroMQ or even Redis.

- Writing logs in file and `tail`ing them via SSH is a mess. Write all the logs
  into (remote) syslog, either your own or SaaS. Syslog brings huge capabilities
  with logs processing.

- Never commit the master branch directly (set it up into your Git config). Use
  the simplest Git pipeline you can imagine:

  ```
  master -> feature-branch -> commits -> pull request -> review -> merge
  ```

### [Programming languages](#lang)

- Prefer those languages that could give you a single compiled file as a result
  of you effort (both binary or bytecode). C-family, Go, Rust, Haskell,
  Java-family are OK. PHP, Python, Ruby, Perl, JavaScript are less OK.

- Take a look at functional languages even you don't have intentions using them
  in your daily work.

- You'd better try not modern languages but rather old ones. Small-talk, Lisp,
  OCaml would be a great choice.

### [Workspace](#workspace)

- Keep you desktop free from unused items.

- The more gadgets you need having around the less you are productive. Ideally,
  you only need your Mac connected to the Internet.

- Use messagers on mobile only except those you need to communicate with your
  customer. On my desktop, I have only Slask running with my customer's
  room. Leave Telegram, Skype, WhatsApp or whatever else on you phone and check
  them rarely.

- Turn off all the notifications on you phone/desktop.

- Try to keep you developing tools simple. Choose text editor like Vim or Emacs
  over IDE. Work with Git from a command line.

- Don't work in open-space. A room with 3-4 people around is OK.

- Don't read the news. Your friends will warn you if something really important
  happens.

### [Communication](#communication)

- Don't argue on Vim vs Emacs, Python vs Ruby and so on. It looks quite
  unprofessional.

- If you full of thoughts you want to share with the world, open a blog or write
  a book. But never argue on them in social networks or messagers.

- Even you are a remote worker, say Hi and Bye every time you've started or
  finished your work day. Your team should know whether are you at the desk or
  not.

- Be always polite.

- When you don't know what to say, keep silence.

- Never afraid saying No.

- Read about negotiations.

- Invest time and money in improving your English skills.
