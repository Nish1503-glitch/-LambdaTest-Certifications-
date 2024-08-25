# -LambdaTest-Certifications-
Test Scenario 1
To test the "Simple Form Demo" on LambdaTest’s Selenium Playground, you can follow these steps using Selenium WebDriver. Below is a sample script in Python using Selenium to accomplish the given test scenario:

Prerequisites
Ensure you have Selenium installed (pip install selenium).
Download the appropriate WebDriver for your browser (e.g., ChromeDriver for Chrome) and ensure it's in your system's PATH.
const { Builder, By, Key, until } = require('selenium-webdriver');
const chrome = require('selenium-webdriver/chrome');
const path = require('chromedriver').path;

(async function testSimpleFormDemo() {
    // Initialize WebDriver (assuming ChromeDriver here)
    let driver = await new Builder()
        .forBrowser('chrome')
        .setChromeOptions(new chrome.Options())
        .build();

    try {
        // Step 1: Open LambdaTest’s Selenium Playground
        await driver.get("https://www.lambdatest.com/selenium-playground");

        // Step 2: Click “Simple Form Demo” under Input Forms
        let simpleFormDemoLink = await driver.findElement(By.linkText("Simple Form Demo"));
        await simpleFormDemoLink.click();

        // Step 3: Validate that the URL contains “simple-form-demo”
        let currentUrl = await driver.getCurrentUrl();
        if (!currentUrl.includes("simple-form-demo")) {
            throw new Error(`URL does not contain 'simple-form-demo': ${currentUrl}`);
        }

        // Step 4: Create a variable for a string value
        let message = "Welcome to LambdaTest";

        // Step 5: Use this variable to enter values in the “Enter Message” text box
        let messageBox = await driver.findElement(By.id("user-message"));
        await messageBox.sendKeys(message);

        // Step 6: Click “Get Checked Value”
        let getCheckedValueButton = await driver.findElement(By.className("btn-primary"));
        await getCheckedValueButton.click();

        // Step 7: Validate whether the same text message is displayed in the right-hand panel
        let displayedMessage = await driver.findElement(By.id("message")).getText();
        if (message !== displayedMessage) {
            throw new Error(`Expected message: ${message}, but got: ${displayedMessage}`);
        }

    } finally {
        // Wait for a while before closing the browser to see the result
        await driver.sleep(5000);
        // Close the WebDriver
        await driver.quit();
    }
})();

Explanation
Open LambdaTest’s Selenium Playground:

Use driver.get() to navigate to the URL.
Click “Simple Form Demo”:

Find the link by its text and click it.
Validate URL:

Use assert to check if the URL contains "simple-form-demo".
Create a variable for a string value:

Define a string variable.
Enter the value into the text box:

Locate the text box by its ID and send the string value to it.
Click “Get Checked Value”:

Locate the button by its class name and click it.
Validate displayed message:

Retrieve the text from the result element and assert it matches the expected message.
Note
Adjust the WebDriver initialization if you're using a different browser (e.g., Firefox, Edge).
The time.sleep(5) is added to give some time to observe the results before the browser closes. You can adjust or remove this based on your needs.

Test Scenario 2

Sure! Here’s a detailed test scenario for the given instructions:

Test Scenario: Drag & Drop Slider Functionality
Objective: Validate that the slider on the "Drag & Drop Sliders" page can be adjusted from a default value of 15 to 95, and ensure that the displayed value updates correctly.

Steps:

Open the Website:

Action: Navigate to https://www.lambdatest.com/selenium-playground.
Expected Result: The page loads successfully.
Navigate to the Drag & Drop Sliders Page:

Action: Find and click on “Drag & Drop Sliders” under the “Progress Bars & Sliders” section.
Expected Result: You are redirected to the “Drag & Drop Sliders” page.
Locate the Slider with Default Value 15:

Action: Identify the slider labeled “Default value 15”.
Expected Result: The slider is present on the page and its default value is displayed as 15.
Adjust the Slider:

Action: Click and hold the slider knob and drag it to adjust the value to 95.
Expected Result: The slider moves smoothly, and the range value updates dynamically.
Verify the Value:

Action: Observe the value displayed next to or below the slider.
Expected Result: The value displayed should be 95, confirming that the slider was correctly adjusted to the desired value.
Test Data:

Initial Slider Value: 15
Target Slider Value: 95
Expected Results:

The slider should start at 15 and be movable to 95.
The displayed value next to or below the slider should accurately show 95 after the adjustment.
Postconditions:

Ensure the slider returns to the default or initial state if necessary for subsequent tests.
Notes:

Check the responsiveness of the slider on different screen sizes if applicable.
Validate that there are no visual glitches or issues when dragging the slider.
This scenario helps ensure that the slider's drag-and-drop functionality works as intended and that the value displayed reflects the slider's position accurately.

test Scenario 3

To test the given scenario using Selenium, follow the steps outlined below. This script assumes you are using Python with the Selenium WebDriver. If you are using a different language or framework, you might need to adapt the syntax accordingly.

First, ensure you have the necessary libraries installed:

bash
Copy code
pip install selenium
Here’s a Python script to accomplish the test scenario:

python
Copy code
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

# Initialize the WebDriver (e.g., Chrome)
driver = webdriver.Chrome()

try:
    # Step 1: Open the specified URL
    driver.get("https://www.lambdatest.com/selenium-playground")

    # Click on "Input Form Submit" under "Input Forms"
    input_form_submit = driver.find_element(By.LINK_TEXT, "Input Form Submit")
    input_form_submit.click()

    # Step 2: Click "Submit" without filling any information
    submit_button = driver.find_element(By.CSS_SELECTOR, "button[type='submit']")
    submit_button.click()

    # Step 3: Assert the error message "Please fill in the fields"
    error_message = WebDriverWait(driver, 10).until(
        EC.visibility_of_element_located((By.CLASS_NAME, "error"))
    )
    assert "Please fill in the fields" in error_message.text

    # Step 4: Fill in the Name, Email, and other fields
    name_field = driver.find_element(By.NAME, "name")
    email_field = driver.find_element(By.NAME, "email")
    phone_field = driver.find_element(By.NAME, "phone")
    address_field = driver.find_element(By.NAME, "address")
    city_field = driver.find_element(By.NAME, "city")
    zip_field = driver.find_element(By.NAME, "zip")

    name_field.send_keys("John Doe")
    email_field.send_keys("johndoe@example.com")
    phone_field.send_keys("1234567890")
    address_field.send_keys("123 Elm Street")
    city_field.send_keys("Springfield")
    zip_field.send_keys("12345")

    # Step 5: Select "United States" from the Country drop-down using the text property
    country_dropdown = driver.find_element(By.NAME, "country")
    country_dropdown.send_keys("United States")

    # Step 6: Click "Submit"
    submit_button.click()

    # Step 7: Validate the success message
    success_message = WebDriverWait(driver, 10).until(
        EC.visibility_of_element_located((By.CLASS_NAME, "success"))
    )
    assert "Thanks for contacting us, we will get back to you shortly." in success_message.text

finally:
    # Close the WebDriver
    driver.quit()
Notes:
WebDriver Setup: Make sure the appropriate WebDriver (e.g., ChromeDriver) is installed and available in your system’s PATH.

Explicit Waits: We use WebDriverWait to handle dynamic content and ensure that elements are visible before interacting with them.

Element Locators: Adjust the locators (By.LINK_TEXT, By.CSS_SELECTOR, By.NAME, etc.) as needed based on the actual HTML structure of the page.

Error Handling: Consider adding more sophisticated error handling and logging for real-world scenarios.

Browser Choice: This script uses ChromeDriver. You can switch to other browsers by changing the WebDriver initialization line and installing the corresponding WebDriver.

Test scenario 3

To test the given scenario using Selenium, follow the steps outlined below. This script assumes you are using Python with the Selenium WebDriver. If you are using a different language or framework, you might need to adapt the syntax accordingly.

First, ensure you have the necessary libraries installed:
const { Builder, By, until } = require('selenium-webdriver');

// Initialize the WebDriver (e.g., Chrome)
let driver = new Builder().forBrowser('chrome').build();

(async function testScenario() {
    try {
        // Step 1: Open the specified URL
        await driver.get("https://www.lambdatest.com/selenium-playground");

        // Click on "Input Form Submit" under "Input Forms"
        let inputFormSubmit = await driver.findElement(By.linkText("Input Form Submit"));
        await inputFormSubmit.click();

        // Step 2: Click "Submit" without filling any information
        let submitButton = await driver.findElement(By.css("button[type='submit']"));
        await submitButton.click();

        // Step 3: Assert the error message "Please fill in the fields"
        let errorMessage = await driver.wait(until.elementLocated(By.className("error")), 10000);
        await driver.wait(until.elementIsVisible(errorMessage), 10000);
        let errorText = await errorMessage.getText();
        console.assert(errorText.includes("Please fill in the fields"), "Error message not found");

        // Step 4: Fill in the Name, Email, and other fields
        let nameField = await driver.findElement(By.name("name"));
        let emailField = await driver.findElement(By.name("email"));
        let phoneField = await driver.findElement(By.name("phone"));
        let addressField = await driver.findElement(By.name("address"));
        let cityField = await driver.findElement(By.name("city"));
        let zipField = await driver.findElement(By.name("zip"));

        await nameField.sendKeys("John Doe");
        await emailField.sendKeys("johndoe@example.com");
        await phoneField.sendKeys("1234567890");
        await addressField.sendKeys("123 Elm Street");
        await cityField.sendKeys("Springfield");
        await zipField.sendKeys("12345");

        // Step 5: Select "United States" from the Country drop-down using the text property
        let countryDropdown = await driver.findElement(By.name("country"));
        await countryDropdown.sendKeys("United States");

        // Step 6: Click "Submit"
        await submitButton.click();

        // Step 7: Validate the success message
        let successMessage = await driver.wait(until.elementLocated(By.className("success")), 10000);
        await driver.wait(until.elementIsVisible(successMessage), 10000);
        let successText = await successMessage.getText();
        console.assert(successText.includes("Thanks for contacting us, we will get back to you shortly."), "Success message not found");

    } finally {
        // Close the WebDriver
        await driver.quit();
    }
})();

Notes:
WebDriver Setup: Make sure the appropriate WebDriver (e.g., ChromeDriver) is installed and available in your system’s PATH.

Explicit Waits: We use WebDriverWait to handle dynamic content and ensure that elements are visible before interacting with them.

Element Locators: Adjust the locators (By.LINK_TEXT, By.CSS_SELECTOR, By.NAME, etc.) as needed based on the actual HTML structure of the page.

Error Handling: Consider adding more sophisticated error handling and logging for real-world scenarios.

Browser Choice: This script uses ChromeDriver. You can switch to other browsers by changing the WebDriver initialization line and installing the corresponding WebDriver.
