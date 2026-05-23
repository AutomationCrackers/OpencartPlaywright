# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: SearchProduct.spec.ts >> Product search test @master @regression
- Location: tests\SearchProduct.spec.ts:38:5

# Error details

```
Error: page.goto: net::ERR_CONNECTION_REFUSED at http://localhost/opencart/upload/
Call log:
  - navigating to "http://localhost/opencart/upload/", waiting until "load"

```

# Test source

```ts
  1  | /**
  2  |  * Test Case: Product Search
  3  |  * 
  4  |  * Tags: @master @regression
  5  |  * 
  6  |  * Steps:
  7  |  * 1) Navigate to the application URL
  8  |  * 2) Enter the product name in the search field
  9  |  * 3) Click the search button
  10 |  * 4) Verify if the product is displayed in the search results
  11 |  */
  12 | 
  13 | import { test, expect } from '@playwright/test';
  14 | import { HomePage } from '../pages/HomePage';
  15 | import { SearchResultsPage } from '../pages/SearchResultsPage';
  16 | import { TestConfig } from '../test.config';
  17 | 
  18 | // Declare reusable variables
  19 | let config: TestConfig;
  20 | let homePage: HomePage;
  21 | let searchResultsPage: SearchResultsPage;
  22 | 
  23 | // Playwright hook - runs before each test
  24 | test.beforeEach(async ({ page }) => {
  25 |   config = new TestConfig(); // Load configuration values like URL and product name
> 26 |   await page.goto(config.appUrl); // Step 1: Navigate to the application
     |              ^ Error: page.goto: net::ERR_CONNECTION_REFUSED at http://localhost/opencart/upload/
  27 | 
  28 |   // Initialize page objects
  29 |   homePage = new HomePage(page);
  30 |   searchResultsPage = new SearchResultsPage(page);
  31 | });
  32 | 
  33 | // Playwright hook - runs after each test (optional cleanup)
  34 | test.afterEach(async ({ page }) => {
  35 |   await page.close(); // Closes the browser tab after test
  36 | });
  37 | 
  38 | test('Product search test @master @regression', async () => {
  39 |   const productName = config.productName;
  40 | 
  41 |   // Step 2 & 3: Enter product name and click Search
  42 |   await homePage.enterProductName(productName);
  43 |   await homePage.clickSearch();
  44 | 
  45 |   // Step 4: Verify that the search results page is displayed
  46 |   expect(await searchResultsPage.isSearchResultsPageExists()).toBeTruthy();
  47 | 
  48 |   // Step 5: Validate if the searched product appears in results
  49 |   const isProductFound = await searchResultsPage.isProductExist(productName);
  50 |   expect(isProductFound).toBeTruthy();
  51 | });
  52 | 
```