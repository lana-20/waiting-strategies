# Waiting Strategies - Appium and Selenium Automation
The repo contains code snippets used in this [post](..medium post..).

### NoSuchElementException
![image](https://github.com/lana-20/waiting-strategies/assets/70295997/e1c91c69-025f-4e77-9919-73266b3b8e3c)

    from selenium.common.exceptions import NoSuchElementException
    ...
    
    def test_demo():
        driver = webdriver.Remote(server_url, caps)
        
        try:
            element = driver.find_element(By.ID, "foo")
            element.click()
        except NoSuchElementException:
            print(driver.page_source)
            raise
        finally:
            driver.quit()

### Static Wait
![image](https://github.com/lana-20/waiting-strategies/assets/70295997/c8497e96-9f6a-4fde-81ae-3dde5f12b2bd)

      def test_login_static_wait():
          time.sleep(3000)
          driver.find_element(login_screen).click()
          
          time.sleep(3000)
          driver.find_element(username).send_keys(AUTH_USER)
          driver.find_element(password).send_keys(AUTH_PASS)
          driver.find_element(login_button).click()
          
          time.sleep(3000)
          driver.find_element(get_logged_in_by(AUTH_USER))

### Implicit Wait
![image](https://github.com/lana-20/waiting-strategies/assets/70295997/a1ed2899-c587-4d12-a974-5c04a1da94b0)

      def test_login_implicit_wait():
          driver.implicitly_wait(10)
          
          driver.find_element(login_screen).click()
          driver.find_element(username).send_keys(AUTH_USER)
          driver.find_element(password).send_keys(AUTH_PASS)
          driver.find_element(login_button).click()
          driver.find_element(get_logged_in_by(AUTH_USER))

### Explicit Wait

**TODO**

<img>

<code>
