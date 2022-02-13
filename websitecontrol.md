This file details how to control webpages with code:

from selenium import webdriver
from selenium.webdriver.support.select import Select
from selenium.webdriver.common.by import By
from dotenv import load_dotenv

#Storing Credentials
- using .env allows credentials to be stored locally and accessed as variables - this can later be encrypted with additional secure env additions
- have passwords stored = to variable

load_dotenv()

# Initialize the driver
driver = webdriver.Chrome(r'C:\Program Files\Google\Chrome\Application\chromedriver.exe')
driver.implicitly_wait(0.5)
driver.get("WHATEVER WEBPAGE YOU WISH TO GO TO")

#ENTER USERNAME/PASSWORD
usernamefunction = (os.environ.get('secretuser'))
passwordfunction = (os.environ.get('secretkey'))

l = driver.find_element(By.NAME, 'username')
l.send_keys(str(usernamefunction))
l = driver.find_element(By.NAME, 'password')
l.send_keys(str(passwordfunction))
clickbutton = driver.find_element(By.NAME, 'Submit')
clickbutton.click()

#EXAMPLES OF CONTROLLING WEBPAGE ELEMENTS

dropdownselect = Select(driver.find_element(By.NAME, 'ControlWidgetUnit_ba18ffac5de1cfc98477938b99650d6d_unit'))
dropdownselect.select_by_visible_text('bps')
seconddropdownselect = Select(driver.find_element(By.NAME, 'ControlWidgetBoundary_00f4638419bbad79e67c63794e889091_boundary'))
seconddropdownselect.select_by_visible_text('Managed Object Boundary')
clickbutton = driver.find_element(By.ID, 'controlBar_update_button')
clickbutton.click()