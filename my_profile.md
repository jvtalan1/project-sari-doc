# My Profile

To retieve user and customer profile information . You can use the **my_profile** API.

My Profile contains the following object:

- user
- customer
  - my_vendors

## GET my_profile

### Command

**GET** /c/api/my_profile

### Returns

```json
{
  "user": {
    "id": "5d08c15c02273817630bb503",
    "email": "customer1@test.com",
    "firstname": "Alexander",
    "lastname": "Great",
    "telephone": "888-8888",
    "mobile": "999-999",
    "user_type": "customer",
    "customer_id": "5d08c15c02273817630bb502"
  },
  "organization": {
    "my_vendors": [],
    "_id": "5d08c15c02273817630bb502",
    "name": "Alexander's Store",
    "created_at": "2019-06-18T10:47:56.736Z",
    "updated_at": "2019-07-13T23:22:42.223Z",
    "__v": 32,
    "mobile": "999-999",
    "telephone": "888-8888",
    "address": "1st Street, BGC",
    "contact": "Mr Handsome"
  }
}
```
