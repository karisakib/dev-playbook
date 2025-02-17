## Testing


### Guide To Testing The Frontend

##### Unit Tests (Jest, Testing Library)

##### E2E Tests (Playwright, Axe)

##### Performance Tests (Lighthouse CLI)

Use Google's Lighthouse CLI to perform frontend performance tests. The goal is to score above 90 on each metric.

### Guide To Testing The Backend

##### Test Data Setup
- Create test users to test permissions
- Create test users to test authentication
- Create test users to test api resources
- Give test user names and personalities

##### Unit Tests


##### Integration Tests

If short on time, prefer integration tests over unit tests because it covers logical workflows ands business logic

Unit test the business logic which is under your control.

Follow the Arrange-Act-Assert pattern in testing.

```javascript
describe("User Service", () => {
 it("Should create a user given correct data", async () => {
  // 1. Arrange - prepare the data, create any objects you need
  const mockUser = {
   // ...
  };
  const userService = createUserService(mockLogger, mockQueryBuilder);

  // 2. Act - execute the logic that you're testing
  const result = userService.create(mockUser);

  // 3. Assert - validate the expected result
  expect(mockLogger).toHaveBeenCalled();
  expect(mockQueryBuilder).toHaveBeenCalled();
  expect(result).toEqual(/** ... */);
 });
});
```

##### Load Tests (Artillery)
