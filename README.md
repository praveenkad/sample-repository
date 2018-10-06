        
	/**
	 * Method -  Method for User Click, waits until the element is loaded
	 * and then performs a click action
	 * 
	 * @param element
	 * @param waitTime
	 * @author Praveen Kadambari
	 */
	public void click(WebElement element, String sElementName, int optionWaitTime) {
		try {
			waitForElementToLoad(element, sElementName, optionWaitTime);
			scrollIntoElementView(element);
			setHighlight(element);
			element.click();
		} catch (StaleElementReferenceException e) {
			log.error("- Element " + sElementName + " is not attached to the page document");
			e.printStackTrace();
			Assert.fail("Element " + sElementName + " is not attached to the page document");
		} catch (NoSuchElementException e) {
			log.error("- Element " + sElementName + " was not found in DOM");
			e.printStackTrace();
			Assert.fail("Element " + sElementName + " was not found in DOM");
		} catch (Exception e) {
			log.error("- Element " + sElementName + " was not clickable in time-"
					+ optionWaitTime);
			e.printStackTrace();
			Assert.fail("Element " + sElementName + " was not clickable in time-" + optionWaitTime);
		}
	}
	
	/**
	 * Method -  Method for User Click, waits until the element is loaded
	 * and then performs a click action
	 * 
	 * @param element
	 * @param locator
	 * @author Praveen Kadambari
	 */
	public void click(By locator, String sElementName, int optionWaitTime) {
	try {
		waitForElementToLoad(locator, sElementName, optionWaitTime);
		scrollIntoElementView(driver.findElement(locator));
		setHighlight(locator);
		driver.findElement(locator).click();
	} catch (StaleElementReferenceException e) {
		log.error("Element " + sElementName + " is not attached to the page document");
		e.printStackTrace();
		Assert.fail("Element " + sElementName + " is not attached to the page document");
	} catch (NoSuchElementException e) {
		log.error("Element " + sElementName + " was not found in DOM");
		e.printStackTrace();
		Assert.fail("Element " + sElementName + " was not found in DOM");
	} catch (Exception e) {
		log.error("Element " + sElementName + " was not clickable in time-"
				+ optionWaitTime);
		e.printStackTrace();
		Assert.fail("Element " + sElementName + " was not clickable in time-" + optionWaitTime);
	}
	}
  
  	/**
	 * Clicks on invisible webelement using java script.
	 * 
	 * @param element
	 * @param i
	 * @author Praveen Kadambari
	 */
	public void nativeClick(WebElement element, String sElementName, int i) {
		try {
			setHighlight(element);
			JavascriptExecutor js = (JavascriptExecutor) driver;
			js.executeScript("arguments[0].click();", element);
			log.info("- clicked on native element " + sElementName);
		} catch (Exception e) {
			log.error("Unable to natively click on the element " + sElementName + " "
					+ e.getStackTrace());
			Assert.fail("Unable to natively click on the element " + sElementName);
		}
	}
  
  	/**
	 * Web driver waits for visibility of web element with specified locator for the amount
	 * of time specified.
	 * @param locator
	 * @param sElementName
	 * @param waitTime
	 * @author Praveen Kadambari
	 * @return true or false
	 */
	public boolean waitForElementToLoad(By locator, String sElementName, int waitTime) {
		try {
			log.info("Waiting until element " + sElementName + " is visible in time "
					+ waitTime + " secs");
			WebDriverWait wait = new WebDriverWait(driver, waitTime);
			wait.until(ExpectedConditions.visibilityOf(driver.findElement(locator)));
		} catch (TimeoutException e) {
			log.error("Element " + sElementName + " was not visible in time - " + waitTime);
			e.printStackTrace();
			Assert.fail("Element " + sElementName + " was not visible in time - " + waitTime);
			return false;
		} catch (NoSuchElementException e) {
			log.error("Element " + sElementName + "is not attached to the page document"
					+ getStackTrace());
			e.printStackTrace();
			Assert.fail("Element " + sElementName + "is not attached to the page document");
			return false;
		} catch (Exception e) {
			e.printStackTrace();
			Assert.fail("Unable to find the element " + sElementName);
			return false;
		}
		return true;
	}

/**
	 * Method -  Method for User Clear and Type, waits until the element is
	 * loaded and then enters some text
	 * 
	 * @param element
	 * @param sText
	 * @param waitTime
	 * @author Praveen Kadambari
	 */
	public void clear(WebElement element, String sElementName, int... optionWaitTime) {
		try {
			int waitTime = getWaitTime(optionWaitTime);
			if (isElementPresent(element, sElementName, waitTime)) {
				scrollIntoElementView(element);
				setHighlight(element);
				element.clear();
				log.info("Cleared the field in the element - " + sElementName);
			} else {
				log.error("Unable to clear field " + sElementName + getStackTrace());
				Assert.fail("Unable to clear field " + sElementName);
			}
		} catch (StaleElementReferenceException e) {
			log.error("Element for " + locatorOf(element)
					+ " is not attached to the page document" + getStackTrace());
			Assert.fail("Element for " + sElementName + " is not attached to the page document");
		} catch (NoSuchElementException e) {
			log.error(
					"Element for " + sElementName + " was not found in DOM" + getStackTrace());
			Assert.fail("Element for " + sElementName + " was not found in DOM");
		} catch (Exception e) {
			log.error("Unable to clear text in field with element -" + sElementName
					+ getStackTrace());
			Assert.fail("Unable to clear text in field with element -" + sElementName);
		}
	}

	/**
	 * Method -  Method for User Clear and Type, waits until the element is
	 * loaded and then enters some text
	 * 
	 * @param element
	 * @param sText
	 * @param waitTime
	 * @author Praveen Kadambari
	 */
	public void clearAndType(WebElement element, String text, String sElementName, int... optionWaitTime) {
		try {
			int waitTime = getWaitTime(optionWaitTime);
			if (isElementPresent(element, sElementName, waitTime)) {
				scrollIntoElementView(element);
				setHighlight(element);
				element.clear();
				element.sendKeys(text);
				log.info("Cleared the field and entered -** " + text + " ** in the element - "
						+ sElementName);
			} else {
				log.error("Unable to clear and enter " + text + " in field " + sElementName
						+ getStackTrace());
				Assert.fail("Unable to clear and enter " + text + " in field " + sElementName);
			}
		} catch (StaleElementReferenceException e) {
			log.error("Element for " + locatorOf(element)
					+ " is not attached to the page document" + getStackTrace());
			Assert.fail("Element for " + sElementName + " is not attached to the page document");
		} catch (NoSuchElementException e) {
			log.error(
					"Element for " + sElementName + " was not found in DOM" + getStackTrace());
			Assert.fail("Element for " + sElementName + " was not found in DOM");
		} catch (Exception e) {
			e.printStackTrace();
			log.error("Unable to clear and enter '" + text + "' text in field with element -"
					+ sElementName + getStackTrace());
			Assert.fail("Unable to clear and enter '" + text + "' text in field with element -" + sElementName);
		}
	}

/**
	 * Purpose- This function lets the webdriver wait until the page loads
	 * completely
	 * @throws TimeoutException
	 * @author Praveen Kadambari
	 */
	public boolean waitForPageToLoad() 
	{
		log.info("- Waiting for page to load");
		try {
			int waitTime = 0;
			boolean isPageLoadComplete = false;
			do {
				isPageLoadComplete = ((String) ((JavascriptExecutor) driver)
						.executeScript("return document.readyState")).equals("complete");
				sleep(1);
				waitTime++;
				if (waitTime > 250) {
					log.info("- Page Load Complete");
					break;
				}
			} while (!isPageLoadComplete);
			{
			}
			// wait.until(ExpectedConditions.visibilityOfAllElementsLocatedBy(By.cssSelector(waitString)));
		} catch (TimeoutException e) {
			return false;
		}catch(Exception e){
			return false;
		}
		return true;
	}
