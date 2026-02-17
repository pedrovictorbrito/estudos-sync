




























.



@@0001

- webdriver creation
    - driver = selenium.webdriver.⎵⎵⎵()
        - Chrome
- url selection
    - selenium.webdriver.⎵⎵⎵(url)
        - get
- driver quitting
    - driver.⎵⎵⎵()
        - quit
- Implicit vs Explicit waiting strategy
    - Implicit = Can be global; Keeps trying the given action till it succeeds
    - Explicit = Per element; Waits for a given state to be reached
- setting implicit waiting globally
    - options = selenium.get_⎵⎵⎵_chrome_options()
        - default
    - driver = selenium.webdriver.Chrome(options=options)
- finding elements
    - selenium.webdriver.⎵⎵⎵(by=By.CSS_SELECTOR, ⎵⎵⎵="h1")
        - find_element (or elements)
        - value
- enter input 
    - element.send_⎵⎵⎵("test")
        - keys
- innerHTML
    - el.get_⎵⎵⎵("innerHTML")
        - attribute
        - or 
- set global implicit waits
    - options = get_default_chrome_options()
    - options.⎵⎵⎵ = { "implicit": 5000 }
        - timeouts

from selenium import webdriver


driver = webdriver.Chrome()

driver.get("http://selenium.dev")

driver.quit()

title = driver.title

driver.implicitly_wait(0.5)

text_box = driver.find_element(by=By.NAME, value="my-text")
submit_button = driver.find_element(by=By.CSS_SELECTOR, value="button")

text_box.send_keys("Selenium")
submit_button.click()

message = driver.find_element(by=By.ID, value="message")
text = message.text

driver.quit()

pytest path/to/test_script.py

    options = get_default_chrome_options()
    options.page_load_strategy = 'normal'
    driver = webdriver.Chrome(options=options)

![Screenshot_20260215_210416_Via](_res/Screenshot_20260215_210416_Via.png)

    options = get_default_chrome_options()
    options.timeouts = { 'implicit': 5000 }
    driver = webdriver.Chrome(options=options)

![Screenshot_20260215_210944_Via](_res/Screenshot_20260215_210944_Via.png)

    wait = WebDriverWait(driver, timeout=2)
    wait.until(lambda _ : revealed.is_displayed())
(Explicit wait strategy)
(Do not mix with implicit wait)