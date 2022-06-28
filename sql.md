
```
DROP TABLE IF EXISTS users CASCADE;

```
### CREATE

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

### INSERT

```
INSERT INTO  brands (name, discount)
VALUES ('bmw', 5), ('nissan', 5);
```

### ALTER
```
• ADD - Add Constraints: Key Unique etc
• SET - Set Column Value
• DROP - Remove Constraints

ALTER TABLES docs
    ADD PRIMARY KEY (id)
    ADD UNIQUE (name)
    
ALTER TABLES docs
    ALTER COLUMN created SET DATA TYME timestamp
    ALTER COLUMN theme DROP NOT NULL
    
```
