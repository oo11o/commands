
```
DROP TABLE IF EXISTS users CASCADE;

```

```
CREATE TABLE users (
    id bigint PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
    email varchar(255),
    first_name varchar(255)
);

```


```
CREATE TABLE order_items (
    id bigint PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
    order_id bigint REFERENCES orders(id),
    price integer,
    good_id bigint REFERENCES goods(id)
);
```
