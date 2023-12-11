# Waiting Strategies - Appium and Selenium Automation
The repo contains code snippets used in this [post](..medium post..).

### NoSuchElementException
![image](https://github.com/lana-20/waiting-strategies/assets/70295997/05899874-b6b0-4909-b724-0fa4db1861e3)

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

![image](https://github.com/lana-20/waiting-strategies/assets/70295997/1de4f618-d576-4d24-9e00-45a3418b395d)

    def test_login_static_wait():
        time.sleep(3)
        driver.find_element(login_screen).click()
        
        time.sleep(3)
        driver.find_element(username).send_keys(AUTH_USER)
        driver.find_element(password).send_keys(AUTH_PASS)
        driver.find_element(login_button).click()
        
        time.sleep(3)
        driver.find_element(get_logged_in_by(AUTH_USER))

### Implicit Wait
![image](https://github.com/lana-20/waiting-strategies/assets/70295997/f5aa8df6-50e7-4774-b1fe-4cdb5a9b2be0)

    def test_login_implicit_wait():
        driver.implicitly_wait(10)
        
        driver.find_element(login_screen).click()
        driver.find_element(username).send_keys(AUTH_USER)
        driver.find_element(password).send_keys(AUTH_PASS)
        driver.find_element(login_button).click()
        driver.find_element(get_logged_in_by(AUTH_USER))

### Explicit Wait

![image](https://github.com/lana-20/waiting-strategies/assets/70295997/3bfe07c0-437c-4802-8720-8e0f46fdca78)

    def test_login_explicit_wait():
        wait = WebDriverWait(driver, 10)
        
        wait.until(expected_conditions.presence_of_element_located(login_screen)).click()
        wait.until(expected_conditions.presence_of_element_located(username)).send_keys(AUTH_USER)
        wait.until(expected_conditions.presence_of_element_located(password)).send_keys(AUTH_PASS)
        wait.until(expected_conditions.presence_of_element_located(login_button)).click()
        wait.until(expected_conditions.presence_of_element_located(get_logged_in_by(AUTH_USER)))


![image](https://github.com/lana-20/waiting-strategies/assets/70295997/fcaf993e-93de-4545-b8a3-aa9140691c08)

    from selenium.webdriver.common.by import By
    from selenium.webdriver.support.ui import WebDriverWait
    from selenium.webdriver.support import expected_conditions as EC
    
    element = WebDriverWait(driver, 10).until(
        EC.presence_of_element_located((By.ID, "foo"))
        )

### Custom Explicit Wait

![image](https://github.com/lana-20/waiting-strategies/assets/70295997/aaf23590-5508-49a0-a937-d7851f6f6c67)

    class tap_is_successful(object):
        
        def __init__(self, locator):
            self.locator = locator
            
            def __call__(self, driver):
                try:
                    element = driver.find_element(*self.locator)
                    element.click()
                    return True
                except:
                    return False
                    
    wait = WebDriverWait(driver, 10)
    wait.until(tap_is_successful(By.ID, "foo"))

![image](https://github.com/lana-20/waiting-strategies/assets/70295997/e543b9b0-8bcf-4681-803e-4f436e5d7d62)

    class element_found_and_clicked(object):
        
        def __init__(self, locator):
            self.locator = locator
            
            def __call__(self, driver):
                try:
                    element = driver.find_element(*self.locator)
                    element.click()
                    return True
                except:
                    return False

![image](https://github.com/lana-20/waiting-strategies/assets/70295997/1762bbd3-f124-44cb-87f1-c02caf5d6a0a)

    def test_login_custom_wait():
        wait = WebDriverWait(driver, 10)
        
        wait.until(element_found_and_clicked(login_screen))
        wait.until(expected_conditions.presence_of_element_located(username)).send_keys(AUTH_USER)
        wait.until(expected_conditions.presence_of_element_located(password)).send_keys(AUTH_PASS)
        wait.until(element_found_and_clicked(login_button))
        wait.until(expected_conditions.presence_of_element_located(get_logged_in_by(AUTH_USER))) 

### Fluent Wait

![image](https://github.com/lana-20/waiting-strategies/assets/70295997/4356ae91-dc93-4e8e-b94f-c98b9dc380a1)

    wait = WebDriverWait(
        driver, timeout=10, poll_frequency=2, ignored_exceptions=ignore_list
        )




