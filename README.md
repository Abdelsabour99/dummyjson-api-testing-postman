# DummyJSON – Products API Testing

Manual and automated API testing of the **Products** endpoints of [DummyJSON](https://dummyjson.com/docs/products), using **Postman**.

## Scope

| Area | Endpoints |
|---|---|
| Read | `GET /products`, `GET /products/{id}`, `GET /products/search` |
| Query options | `limit`, `skip`, `select`, `sortBy`, `order`, `modifiedAfter`, `modifiedBefore` |
| Categories | `GET /products/categories`, `GET /products/category-list`, `GET /products/category/{name}` |
| Write (simulated) | `POST /products/add`, `PUT` / `PATCH /products/{id}`, `DELETE /products/{id}` |

## What is in this repo

- `test-cases/Api_Testing_DummyJason.xlsx`
  - **TC sheet:** 85 test cases (ID, title, method, endpoint, body, priority, severity, expected result, actual result, status).
  - **Bug sheet:** defects found, with steps to reproduce, expected vs. actual result, and the related test case ID.
- `postman/DummyJSON_API_Testing_Portfolio_postman_collection.json`
  - One request per test case, named with its TC ID (for example `TC_PROD_026 - Get Products with limit and skip`).
  - Automated assertions on status code, response body, data types, sorting, pagination, and response time.
- `screenshots/` – Postman Runner results and sample bug evidence.

## Test design

- **Positive, negative, and boundary** cases for every endpoint.
- Pagination and query options: `limit=0`, `limit` above the total, `skip` beyond the total, negative and non-numeric values.
- Sorting checked in both directions on text and numeric fields.
- Date filters (`modifiedAfter`, `modifiedBefore`) checked with past, future, and invalid dates.
- Data handling: missing, null, empty, and wrong-type fields; Unicode text; an SQL-injection-style string.
- Persistence checks: DummyJSON simulates POST, PUT, and DELETE without saving, so these tests verify that behavior against the docs.

## How to run

1. Import the collection into Postman.
2. Create a collection variable (or an environment variable) named `Base URL` with the value `https://dummyjson.com/` (keep the trailing slash).
3. Open the collection, click **Run**, and run all requests.

## Results summary

| Total test cases | Passed | Failed | Bugs reported |
|---|---|---|---|
| 85 | [X] | [X] | [X] |

**Main finding:** [one sentence, for example: the API accepts invalid POST bodies (missing title or price, wrong types) and returns 201 Created instead of 400 Bad Request.]

## Notes

- Where the DummyJSON docs do not define a behavior (for example a negative `limit`), the expected result follows REST best practice and is marked as such in the test case.
- Test cases are tied to Postman requests by TC ID, and bugs are tied to test cases by TC ID, so every result is traceable.

## Tools

Postman · Excel · JSON · REST API testing

## Author

**Abdelsabour Mohamed** – Junior QA Engineer
[LinkedIn](https://www.linkedin.com/in/abdelsabour-elqady-1a9334258) · [GitHub](https://github.com/Abdelsabour99)
