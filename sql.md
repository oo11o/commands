DROP TABLE IF EXISTS users CASCADE;

CREATE TABLE users (
    id bigint PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
    email varchar(255),
    first_name varchar(255)
);
