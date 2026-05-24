# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: AccountRegistration.spec.ts >> User registration test @master @sanity @regression
- Location: tests\AccountRegistration.spec.ts:99:5

# Error details

```
Error: page.goto: net::ERR_CONNECTION_REFUSED at http://localhost/opencart/upload/
Call log:
  - navigating to "http://localhost/opencart/upload/", waiting until "load"

```

# Test source

```ts
  1   | /**
  2   |  * Test Case: Account Registration
  3   |  * 
  4   |  * Tags: @master @sanity @regression
  5   |  * 
  6   |  * Steps:
  7   |  * 1) Navigate to application URL 
  8   |  * 2) Go to 'My Account' and click 'Register'
  9   |  * 3) Fill in registration details with random data
  10  |  * 4) Agree to Privacy Policy and submit the form
  11  |  * 5) Validate the confirmation message
  12  |  */
  13  | 
  14  | import { test, expect } from '@playwright/test';
  15  | import { HomePage } from '../pages/HomePage';
  16  | import { RegistrationPage } from '../pages/RegistrationPage';
  17  | import { RandomDataUtil } from '../utils/randomDataGenerator';
  18  | import { TestConfig } from '../test.config';
  19  | 
  20  | /* test('User registration', async ({page}) => {
  21  | 
  22  | const config = new TestConfig();
  23  | await page.goto(config.appUrl);
  24  | 
  25  | const homePage = new HomePage(page);
  26  | await homePage.clickMyAccount();
  27  | await homePage.clickRegister();
  28  | 
  29  | const registrationPage = new RegistrationPage(page);
  30  | await registrationPage.setFirstName(RandomDataUtil.getFirstName());
  31  | await registrationPage.setLastName(RandomDataUtil.getlastName());
  32  | await registrationPage.setEmail(RandomDataUtil.getEmail());
  33  | await registrationPage.setTelephone(RandomDataUtil.getPhoneNumber());
  34  | 
  35  | const password = RandomDataUtil.getPassword();
  36  | await registrationPage.setPassword(password);
  37  | await registrationPage.setConfirmPassword(password);
  38  | 
  39  | await registrationPage.setPrivacyPolicy();
  40  | await registrationPage.clickContinue();
  41  | 
  42  | const confirmationMsg = await registrationPage.getConfirmationMsg();
  43  | expect(confirmationMsg).toContain('Your Account Has Been Created!');
  44  | 
  45  | await page.waitForTimeout(3000);
  46  | })
  47  |  */
  48  | /**************************************************** */
  49  | let homePage: HomePage;
  50  | let registrationPage: RegistrationPage;
  51  | let config: TestConfig;
  52  | 
  53  | test.beforeEach(async ({ page }) => {
  54  |     config = new TestConfig();
> 55  |     await page.goto(config.appUrl); //Navigate to application URL 
      |                ^ Error: page.goto: net::ERR_CONNECTION_REFUSED at http://localhost/opencart/upload/
  56  |     homePage = new HomePage(page);
  57  |     registrationPage = new RegistrationPage(page);
  58  | 
  59  | })
  60  | 
  61  | 
  62  | test.afterEach(async ({ page }) => {
  63  | 
  64  |     await page.waitForTimeout(3000);
  65  |     await page.close();
  66  | 
  67  | })
  68  | /*
  69  | //not using any page fixture inside test so no ned to pass
  70  | test('User registration test with hooks', async () => {
  71  | 
  72  |     //Go to 'My Account' and click 'Register'
  73  | 
  74  |     await homePage.clickMyAccount();
  75  |     await homePage.clickRegister();
  76  | 
  77  |     //Fill in registration details with random data
  78  |     await registrationPage.setFirstName(RandomDataUtil.getFirstName());
  79  |     await registrationPage.setLastName(RandomDataUtil.getlastName());
  80  |     await registrationPage.setEmail(RandomDataUtil.getEmail());
  81  |     await registrationPage.setTelephone(RandomDataUtil.getPhoneNumber());
  82  | 
  83  |     const password = RandomDataUtil.getPassword();
  84  |     await registrationPage.setPassword(password);
  85  |     await registrationPage.setConfirmPassword(password);
  86  | 
  87  |     await registrationPage.setPrivacyPolicy();
  88  |     await registrationPage.clickContinue();
  89  | 
  90  |     //Validate the confirmation message
  91  | 
  92  |     const confirmationMsg = await registrationPage.getConfirmationMsg();
  93  |     expect(confirmationMsg).toContain('Your Account Has Been Created!')
  94  | 
  95  | 
  96  | })
  97  | */
  98  |  //test with tags
  99  | test('User registration test @master @sanity @regression', async () => {
  100 | 
  101 |     //Go to 'My Account' and click 'Register'
  102 | 
  103 |     await homePage.clickMyAccount();
  104 |     await homePage.clickRegister();
  105 | 
  106 |     //Fill in registration details with random data
  107 |     await registrationPage.setFirstName(RandomDataUtil.getFirstName());
  108 |     await registrationPage.setLastName(RandomDataUtil.getlastName());
  109 |     await registrationPage.setEmail(RandomDataUtil.getEmail());
  110 |     await registrationPage.setTelephone(RandomDataUtil.getPhoneNumber());
  111 | 
  112 |     const password = RandomDataUtil.getPassword();
  113 |     await registrationPage.setPassword(password);
  114 |     await registrationPage.setConfirmPassword(password);
  115 | 
  116 |     await registrationPage.setPrivacyPolicy();
  117 |     await registrationPage.clickContinue();
  118 | 
  119 |     //Validate the confirmation message
  120 | 
  121 |     const confirmationMsg = await registrationPage.getConfirmationMsg();
  122 |     expect(confirmationMsg).toContain('Your Account Has Been Created!')
  123 | 
  124 | 
  125 | })
  126 |  
```