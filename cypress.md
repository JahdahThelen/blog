# Cypress
8 March 2023

## From the documentation

- Custom comands should NOT use the UI ([Watch video](https://youtu.be/5XQOK0v_YRE?t=943))
- If the __content__ of the element changes, should the test fail? ([See docs](https://docs.cypress.io/guides/references/best-practices#Selecting-Elements))
    - Yes. use `cy.contains()`
    - No. use data attributes
- Automatic cleanup after a tests include: ([See docs](https://docs.cypress.io/guides/core-concepts/test-isolation#Test-Isolation-Enabled))
    - clearing the dom state by visiting `about:blank`
    - clearing cookies in all domains
    - clearing `localStorage` in all domains
    - clearing `sessionStorage` in all domains
- Try out the `testing-library` ([See docs](https://docs.cypress.io/guides/references/best-practices#Cypress-and-Testing-Library))
- Specify an alternative config file to unclutter the root directory ([See docs](https://docs.cypress.io/guides/references/best-practices#Cypress-and-Testing-Library))
- In need of synchronous operations? Use `Cypress.$` ([See docs](https://docs.cypress.io/guides/core-concepts/introduction-to-cypress#2-A-set-timeout-is-reached))
- A chain of command should always end after an action ([See docs](https://docs.cypress.io/guides/core-concepts/introduction-to-cypress#Some-commands-require-a-previous-subject))
- Place synchronous commands within `then()` ([See docs](https://docs.cypress.io/guides/core-concepts/introduction-to-cypress#Mixing-Async-and-Sync-code))
- Implicit assertion can avoid a lot of `expect()` and `should()` ([See docs](https://docs.cypress.io/guides/core-concepts/introduction-to-cypress#Implicit-Assertions))
- There is no need to use `should('exist')` ([See docs](https://docs.cypress.io/guides/core-concepts/introduction-to-cypress#Implicit-Assertions))

## Practical Considerations

### 1. Unique accounts for each test

When accounts are shared between tests they can differ from their initial definition. This can cause confusion about the test requirements. Also, changing the order of tests can break tests. Even though, creating accounts for every test case may seem overkill. 

`cypress/fixtures/accounts.ts`

```ts
export class Account {
    email: string;
    role?: Role;
    profile?: Profile; // Extra account data to not clutter the Account class
    // All test accounts should have the same password, so no password needed

    constructor (
        email: string,
        role?: Role = null,
        profile?: Profile = null
    ) {
        this.email = email;
        this.role = role;
        this.profile = profile;
    }
}
```

`cypress/e2e/tests/a-tests.cy.ts`

```ts
import Account from '@cypress/fixtures/accounts';

// Define accounts used for the test together with the test, as they will only change together
const accounts = {
    happy: new Account('happy@a-test.cypress'),
    edgeCase: new Account('edge-case@a-test.cypress'),
    error: new Account('error@a-test.cypress'),
}

describe('a test', () => {

    [accounts.happy, accounts.edgeCase].forEach((account) => {
        it(`should pass for ${account.email}`, () => {
            cy.test(account)
            .should('pass');
        });
    });

    [accounts.error].forEach((account) => {
        it(`should fail for ${account.email}`, () => {
            cy.test(account)
            .should('fail');
        });
    });
});
```

### 2. Check if all accounts exist prior to the tests

No test will pass if the required accounts do not exist, or have the wrong settings. Checking it beforehand can avoid confusion and debugging when the tests fail.

`cypress/fixtures/accounts.ts`

```ts
... // Account definition

export class Accounts {
    static admin = new Account('admin@global.cypress')
}
```

`cypress/fixtures/a-test.cy.ts`

```ts
... // imports and accounts definition

describe('before a test', () => {
    it('verifies all accounts exist for the test', () => {
        cy.login(Accounts.admin.email);
        cy.accountExists(accounts.happy); // no loop to improve readability
        cy.accountExists(accounts.edgeCase);
        cy.accountExists(accounts.error);
    });
});

... // other tests
```

## Issues

### Using `Before()` skips all other tests

Apparantly, this can happen when the `before()` fails. The test is displayed as succeeded. Weird.
