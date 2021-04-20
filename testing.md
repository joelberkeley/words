# testing

todo a new approach - explain why these important qualities are important, then tag all the recommendations with the relevant qualities

### important qualities of tests

#### readable

#### reproducible

#### accurate

#### maintainable

#### comprehensive

Providing meaningful test coverage

- Don't stop at testing the [happy paths](https://en.wikipedia.org/wiki/Happy_path). They only constitute part of the API. Also test behaviour for unhappy paths. 
- When reviewing changes, check for test coverage. If it’s unclear what’s tested and what’s not, consider making the tests more readable.
- Automated test coverage checks can tell you when your tests are lacking, but they can't tell you when they're complete. For example, they don't measure whether the tests make meaningful assertions. Since they tend to instill overconfidence, I don't recommend them.
- We want to keep test coverage meaningful. For example:
  - Avoid duplicate tests, which create unnecessary maintenance overhead, make running tests slower, and can indicate an inconsistent approach to coverage.
  - Ensure tests are named in meaningfully and accurately. This makes it easier for others to find relevant tests rather than creating duplicates.
  - Add comments to parameterised test cases, ensuring the comments can’t drift. This helps others see which sets of parameters have already been tested.
  - Ensure test setup is correct, as if incorrect it can lead to tests that do not check the behaviour you expect.
  - Test a range of potential inputs, including edge cases and invalid values.
  - Tests that fail intermittently don’t convey meaningful information and as such they reduce developer confidence in the value of tests and the build system. If they are unfixable, it is better to delete them than have them intermittently failing.

### Avoiding bugs in tests

- Write tests alongside the source code. This prevents errors in understanding, keeping a tight loop between development and testing. This also helps to ensure code is designed with the user in mind.
- Keep tests simple. Tests are about confidence, and it's difficult to be confident about complex code. If a test defers part of its work to another source, such as another library or utility function, also test that source.
- When testing non-deterministic objects, take care not to rely on determinism where it can’t be found.

### Make the most of tools

Common techniques

- Mock anything you're not testing. This keeps tests relevant to the functionality under test, and those who read the test can easily work out what is being tested. That said, avoid patching as it typically breaks encapsulation.

Make test suites easy to navigate

A unit test tests one behaviour of a single importable item from the public API. An integration test tests the interaction of several such items. Structure unit tests as a mirror of source code. Store integration tests separately from unit tests.

Make tests easy to read

When reviewing tests, check if you understand what they do and how they’re laid out. If you don’t understand what each individual test point does, or what test points are in a module and how they are structured, it’s likely others won’t either, and they may prove difficult to maintain.

Make tests robust to change

We want to be able to change the implementation behind any piece of functionality with confidence that we aren’t breaking the contract offered in that functionality. Tests that assume a particular implementation make this difficult. For this reason, test the contract not the implementation. In other words test the required properties of the input and output of a piece of functionality, along with any documented side effects (the 'contract'); but avoid making the tests rely on anything implementation-specific.
For example, don't use private members of modules and classes, and don't patch objects used internally in a method or class. If the implementation is complex and needs testing, consider pulling functionality out into an external object, such as a separate function or class, whose contract can be tested separately.

Make tests fast

A user should be able to comfortably run all the tests. If a test is slow, try to speed it up.

Make tests independent

Tests that depend on other tests are hard to reason about, maintain, and diagnose on failure. For this reason, a test should never depend in any way on another test. Consequently,
- don’t rely on the order in which tests are run
- clean up resources and state (global configuration) after a test is complete

Keep to one concept per test

Test only one concept per test. This may require your best judgement for what “one concept” is in a given situation. Try to describe your test. If you use conjunctions, you probably need to break it up. If we do this, each test will only fail for one reason: when changes are made to the source code, only the relevant tests will fail. It also makes it easier to read tests as each test case is captured in its own scope. If you find that this leads to unnecessary duplication in your test code, consider using test utilities or parametrized tests.

When your test framework relies on exceptions for assertions, you can only see as far in the test failure logs as the first failed assert in a test point. In this case, to mitigate this limitation, keep the number of asserts in a test function to a minimum, and ideally just one.

Glossary

- mock (also stub, dummy, double, fake) _n_. A mock of an object has the same interface as the original object (or a subset thereof), but the logic in the original is replaced in the mock with the minimal logic required for the test to work. 
- patch _v_. for an object defined in a given scope, replace any usage of that object within that scope with another object. For example, if I am testing a function which makes a value of type `Foo`, I can patch `Foo` for that function’s enclosing module and test how the function makes use of `Foo`.

Appendix A: Mission statement

- evaluate and communicate the degree to which code works as intended, by ...
  - providing meaningful test coverage
  - avoiding bugs in tests
  - encouraging attention to test failures
- make tests quick and easy to write, by ...
  - making the most of testing tools and techniques
  - writing tests alongside the source code
- make tests quick and easy to maintain, by ...
  - making test suites easy to navigate
  - making tests easy to read
  - making tests robust to change
  - making tests that fail only when there's a genuine problem in the code
- make tests quick and easy to run, by ...
  - making test suites easy to navigate
  - making tests run fast
  - making tests repeatable
- make test failures quick and easy to diagnose, by ...
  - making tests independent
  - keeping to one concept per test

We use these goals to guide us in improving our testing capability. They help us focus on what's helpful, by reminding us to ask ourselves where, when and why testing is useful.
