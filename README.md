# flipkart_mobile_webscrapping
from openpyxl import Workbook
from selenium.webdriver.common.by import By
import selenium
import xlsxwriter
from selenium import webdriver
from selenium import webdriver as wb
from webdriver_manager.chrome import ChromeDriverManager
webD=wb.Chrome(ChromeDriverManager().install())
webD.get('https://www.flipkart.com/')
element_list=[]
details=[]
for page in range(1,525,1):
    page_url='https://www.flipkart.com/search?q=mobiles&as=on&as-show=on&otracker=AS_Query_TrendingAutoSuggest_1_0_na_na_na&otracker1=AS_Query_TrendingAutoSuggest_1_0_na_na_na&as-pos=1&as-type=TRENDING&suggestionId=mobiles&requestId=405f0972-b81f-43d7-8c25-a4a11da42fdd&page='+str(page)
    webD.get(page_url)
    brand=webD.find_elements(By.XPATH,"//div[contains(@class,'_4rR01T')]")
    description=webD.find_elements(By.XPATH,"//div[contains(@class,'fMghEO')]")
    present_price=webD.find_elements(By.XPATH,"//div[contains(@class,'_30jeq3 _1_WHN1')]")
    actual_price=webD.find_elements(By.XPATH,"//div[contains(@class,'_3I9_wc _27UcVY')]")
    rat_rev=webD.find_elements(By.XPATH,"//span[contains(@class,'_2_R_DZ')]")
    stars=webD.find_elements(By.XPATH,"//div[contains(@class,'_3LWZlK')]")
    image_url=webD.find_elements(By.XPATH,"//img[contains(@class,'_396cs4 _3exPp9')]")
    
    for  i in range(len(actual_price)):
        element_list.append([present_price[i].text,stars[i].text])
        details.append({'brand':brand[i].text,'description':description[i].text,'present_price':present_price[i].text,'actual_price':actual_price[i].text,'rat_rev':rat_rev[i].text,'stars':stars[i].text,'image_url':image_url[i].get_attribute('src')})
