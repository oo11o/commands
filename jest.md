### test random function

```
test('buildUser fields', () => {
  const user1 = buildUser();
  expect(user1).toEqual(expect.objectContaining({
    email: expect.any(String),
    firstName: expect.any(String),
    lastName: expect.any(String),
  }));
});

test('buildUser random', () => {
  const user1 = buildUser();
  const user2 = buildUser();
  expect(user1).not.toEqual(user2);
});

test('buildUser override', () => {
  const newData1 = {
    email: 'test@email.com',
  };
  const user1 = buildUser(newData1);
  expect(user1).toMatchObject(newData1);
});

```

### test each file

```
const formats = ['csv', 'json', 'yml'];
const getFixturePath = (name) => path.join(__dirname, '..', '__fixtures__', name);

let expected;

beforeAll(async () => {
  expected = await fs.readFile(getFixturePath('result.html'), 'utf-8');
});

test.each(formats)('%s', async (format) => {
  const filePath = getFixturePath(`list.${format}`);
  const actual = await toHtmlList(filePath);
  expect(actual).toEqual(expected.trim());
});
```
