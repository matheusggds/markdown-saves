# Tests
Following [Willan Justen](https://willianjusten.com.br/) TDD Course here I wil point some usefull informations about it

## Why test?
- Less time spent analysing and correcting bugs
- Easely refactoration
- Documentation
- Better Code design 
- Guarantee quality

## How TDD flow
![TDD flow](https://image.prntscr.com/image/IGyO3DfnRJOV-YtkWYdpXQ.png)

1) Write a code that fails <br>
Write the test, which will fail

2) Make code works <br>
Write the code, simple code (maybe stupid), that the test validates.
 Always a lot of tests for a method, not inverse

3) Refactor

### Test flow
1. Write the test, which obviously will fail
2. Makes the code be validated by test, on a stupid way
3. Write another test for this method
4. Makes the code be validated
5. Write another test, if u want
6. Refactor your code <br>
Garantee your code still valid in a better style

### Think as a Test
1. What the method should do? <br>
All method need to do one thing
2. What data this method will receive?
3. What this method must return?
4. When will this method run?

### Test Pattern
"It should do that when this" <br>
ex.: 
```javascript
it('should return 4 when receive 2,2') {
    expect(sum(2,2)).to.equal(4);
}
```

ex.: `it must add class Active when clicked`

### Test types
![test-pyramid](https://martinfowler.com/bliki/images/testPyramid/test-pyramid.png)

Pyramid created by Martin Fowler, TDD Creator

**Unit** - Simple and little test that validate only one method

- Unit test, tests with unique responsable, if return this or something
- A lot of tests
- Very fast

Tips:
- Isolate it, all test must be independent
- Use `before it` and `after it` to clean global variables
- Use the best asserts ex.: `expected to be`
- Use _Mocks_ to extern calls
- Use test to help your test design

**Service** - Integration test, test to validate if your components work good 

- Integration tests, API responsable, services and etc..
- Not to much tests
- Medium velocity

Tips:
- Careful to dont repeat unit tests
- Isolate it

**UI** - 

- UI Test, Selenium or Phantom JS where u see the machine manipulating the project. 
- Just some tests
- Slow tests

--- 

## Modern React Testing

### Why Automate Testing
- **Confidence to change code**: well-written tests allow you to refactor code with confidence that you’re not breaking anything, and without wasting time updating the tests.

- **Documentation**: tests explain how code works and what’s the expected behavior. Tests, in comparison to any written documentation, are always up to date.

- **Bugs and regression prevention**: by adding test cases for every bug, found in your app, you can be sure that these bugs will never come back. Writing tests will improve your understanding of the code and the requirements, you’ll critically look at your code and find issues that you’d miss otherwise.

### What to teste

The testing trophy, introduced by Kent C. Dodds is getting popular for the frontend tests:

![testing trophy](https://d33wubrfki0l68.cloudfront.net/c4344c0b515b9dd841e4cbaab8aae1f7d422cc67/87f14/images/testing-trophy.svg)

It says that integration tests give you the biggest return on investment, so you should write more integration tests than any other kinds of tests.

*End-to-end* tests in the trophy mostly correspond to UI tests in the pyramid. Integration tests verify big features or even whole pages but without any backend, a real database or a real browser. For example, render a login page, type a username and a password, click the “Log in” button and verify that the correct network request was sent, but without actually making any network requests — we’ll learn how to do it later.

Even if integration tests are more expensive to write, they have several benefits over unit tests:

**Unit tests**

1. One test covers only one module
2. Often require rewrite after refactoring
2. Hard to avoid testing implementation details

**Integration tests**

1. One test covers a whole feature or a page
2. Survive refactoring most of the time
2. Better resemble how users are using your app

_The last point is important: integration tests give us the most confidence that our app works as expected. But it doesn’t mean, that we should only write integration tests. Other tests have their place but we should focus our efforts on tests, that are the most useful._

Now, let’s look closely at each testing trophy level, from the very bottom:

1. **Static analysis** catches syntax errors, bad practices and incorrect use of APIs:  — Code formatters, like Prettier;  — Linters, like ESLint;  — Type checkers, like TypeScript and Flow.

2. **Unit tests** verify that tricky algorithms work correctly. Tools: Jest.
3. **Integration** tests give you confidence that all features of your app work as expected. Tools: Jest and Enzyme or react-testing-library.
4. **End-to-end tests** make sure that your app work as a whole: the frontend and the backend and the database and everything else. Tools: Cypress.

