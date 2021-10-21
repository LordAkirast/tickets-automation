#Imports
#!pip install pyinstaller
from time import sleep
from selenium import webdriver
from selenium.webdriver.common.keys import Keys

import time
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from datetime import date
from datetime import datetime
now = datetime.now()

current_time = now.strftime("%H:%M:%S")


# Import date class from datetime module
today = date.today()


#STEP 1: Acessing OTRS
navegador = webdriver.Chrome("chromedriver.exe")
navegador.maximize_window()
navegador.get("https://otrs.mngs.com.br/otrs/index.pl")
#Acessing OTRS
time.sleep(0.2)
navegador.find_element_by_xpath('//*[@id="User"]').send_keys(#here goes the username)
#Login entered
time.sleep(0.2)
navegador.find_element_by_xpath('//*[@id="Password"]').send_keys(#here goes the password)
#password entered
time.sleep(0.4)
navegador.find_element_by_xpath('//*[@id="LoginButton"]').send_keys(Keys.ENTER)
time.sleep(1)
#Passo 2: Pegar o número de chamados abertos da triagem.
#Chamados > Triagem
navegador.get("https://otrs.mngs.com.br/otrs/index.pl?Action=AgentTicketQueue;QueueID=1;View=;Filter=Unlocked")
time.sleep(1)

#Stores the number of tickets in the variable Chamados Abertos (open tickets)
chamadosAbertos = navegador.find_element_by_xpath('//*[@id="OverviewControl"]/div/div[1]/ul[1]/li[1]/a/span').text

count = 1
while count < 6:

    #Searches the tickets of each consultant and stores their value in the variable "chamados(consultant name)" eg. chamadosDaniel
    navegador.find_element_by_xpath('//*[@id="nav-Tickets"]/a').click()
    navegador.find_element_by_xpath('//*[@id="nav-Tickets-Search"]/a').click()
    time.sleep(2)
    navegador.find_element_by_xpath('//*[@id="SearchProfile_Search"]').send_keys("Chamados Por Consultor")
    time.sleep(2)
    navegador.find_element_by_xpath('//*[@id="SearchProfile_Search"]').send_keys(Keys.DOWN, Keys.ENTER)
    time.sleep(2)
    navegador.find_element_by_xpath('//*[@id="SearchInsert"]/div[4]/div/div/div/div[2]/a').click()
    time.sleep(2)
    
    if count == 1:
        #Choose Daniel's tickets
        navegador.find_element_by_xpath('//*[@id="OwnerIDs_Search"]').click()
        time.sleep(3)
        navegador.find_element_by_xpath('//*[@id="OwnerIDs_Search"]').send_keys(Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.ENTER)
        navegador.find_element_by_xpath('//*[@id="SearchFormSubmit"]/span').click()
        chamadosDaniel = navegador.find_element_by_xpath('//*[@id="OverviewControl"]/div/div[2]/div/span').text
        #Code to leave only last ticket numbers instead of 1-14 it shows 14.
        chamadosDaniel = chamadosDaniel[7:10].strip()
        count = count + 1
        

    elif count == 2:
        #Choose Felipe's tickets
        navegador.find_element_by_xpath('//*[@id="OwnerIDs_Search"]').click()
        time.sleep(3)
        navegador.find_element_by_xpath('//*[@id="OwnerIDs_Search"]').send_keys(Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.ENTER)
        navegador.find_element_by_xpath('//*[@id="SearchFormSubmit"]/span').click()
        chamadosFelipe = navegador.find_element_by_xpath('//*[@id="OverviewControl"]/div/div[2]/div/span').text
        #Code to leave only last ticket numbers instead of 1-14 it shows 14.
        chamadosFelipe = chamadosFelipe[7:10].strip()
        count = count + 1
        
    elif count == 3:
        #Choose Guilherme's tickets
        navegador.find_element_by_xpath('//*[@id="OwnerIDs_Search"]').click()
        time.sleep(3)
        navegador.find_element_by_xpath('//*[@id="OwnerIDs_Search"]').send_keys(Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.ENTER)
        navegador.find_element_by_xpath('//*[@id="SearchFormSubmit"]/span').click()
        chamadosGuilherme = navegador.find_element_by_xpath('//*[@id="OverviewControl"]/div/div[2]/div/span').text
        #Code to leave only last ticket numbers instead of 1-14 it shows 14.
        chamadosGuilherme = chamadosGuilherme[7:10].strip()
        count = count + 1
    
    elif count == 4:
        #Choose Ismael's tickets
        navegador.find_element_by_xpath('//*[@id="OwnerIDs_Search"]').click()
        time.sleep(3)
        navegador.find_element_by_xpath('//*[@id="OwnerIDs_Search"]').send_keys(Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.ENTER)
        navegador.find_element_by_xpath('//*[@id="SearchFormSubmit"]/span').click()
        chamadosIsmael = navegador.find_element_by_xpath('//*[@id="OverviewControl"]/div/div[2]/div/span').text
        #Code to leave only last ticket numbers instead of 1-14 it shows 14.
        chamadosIsmael = chamadosIsmael[7:10].strip()
        count = count + 1
    
    elif count == 5:
        #Choose Kleber's tickets
        navegador.find_element_by_xpath('//*[@id="OwnerIDs_Search"]').click()
        time.sleep(3)
        navegador.find_element_by_xpath('//*[@id="OwnerIDs_Search"]').send_keys(Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN,Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.DOWN, Keys.ENTER)
        navegador.find_element_by_xpath('//*[@id="SearchFormSubmit"]/span').click()
        chamadosKleber = navegador.find_element_by_xpath('//*[@id="OverviewControl"]/div/div[2]/div/span').text
        #Code to leave only last ticket numbers instead of 1-14 it shows 14.
        chamadosKleber = chamadosKleber[7:10].strip()
        count = count + 1


        #Shows open tickets in queue screening by consultant
logopenticket = print("\n Há",chamadosAbertos,"chamados abertos na triagem desbloqueados.")
logopenticketda = print("\nO Consultor Daniel tem:",chamadosDaniel,"chamados abertos.")
logopenticketfe = print("\nO Consultor Felipe tem:",chamadosFelipe,"chamados abertos.")
logopenticketgu = print("\nO Consultor Guilherme tem:",chamadosGuilherme,"chamados abertos.")
logopenticketis = print("\nO Consultor Ismael tem:",chamadosIsmael,"chamados abertos.")
logopenticketkl = print("\nO Consultor Kleber tem:",chamadosKleber,"chamados abertos.")
print("\n")

if len(chamadosDaniel) > 23:
    #Turn it to STR, just take the number and turn it into INT again to count down there
    chamadosDaniel = chamadosDaniel[7:10].strip()
    chamadosDaniel = int(chamadosDaniel)

elif len(chamadosFelipe) > 23:
    #Turn it to STR, just take the number and turn it into INT again to count down there
    chamadosFelipe = chamadosFelipe[7:10].strip()
    chamadosFelipe = int(chamadosFelipe)

elif len(chamadosGuilherme) > 23:
    #Turn it to STR, just take the number and turn it into INT again to count down there
    chamadosGuilherme = chamadosGuilherme[7:10].strip()
    chamadosGuilherme = int(chamadosGuilherme)

elif len(chamadosIsmael) > 23:
    #Turn it to STR, just take the number and turn it into INT again to count down there
    chamadosIsmael = chamadosIsmael[7:10].strip()
    chamadosIsmael = int(chamadosIsmael)

elif len(chamadosKleber) > 23:
    #Turn it to STR, just take the number and turn it into INT again to count down there
    chamadosKleber = chamadosKleber[7:10].strip()
    chamadosKleber = int(chamadosKleber)


#Code to get only numbers from tickets and avoid getting strings
chamadosDaniel = int((chamadosDaniel))
chamadosFelipe = int((chamadosFelipe))
chamadosIsmael = int((chamadosIsmael))
chamadosKleber = int((chamadosKleber))
chamadosGuilherme = int((chamadosGuilherme))

 #code to get the average number of calls per consultant
media = float((int(chamadosDaniel) + int(chamadosFelipe) + int(chamadosGuilherme) + int(chamadosIsmael) + int(chamadosKleber)))/5
media = media + 10

#Set the variables below to the bottom to see if they need help or not. If yes, the value changes to 1.
dahelp = 0
fehelp = 0
guhelp = 0
ishelp = 0
klhelp = 0

#comparison of who needs help
if int(chamadosGuilherme) > media:
    loghelpgu = str(print("\nO Consultor Guilherme precisa de ajuda!",chamadosGuilherme,"Chamados"))
    guhelp = 1
    

if int(chamadosDaniel) > media:
    loghelpda = str(print("\nO Consultor Daniel precisa de ajuda!",chamadosDaniel,"Chamados"))
    dahelp = 1
  
        
if int(chamadosFelipe) > media:
    loghelpfe = str(print("\nO Consultor Felipe precisa de ajuda!",chamadosFelipe,"Chamados"))
    fehelp = 1
    

if int(chamadosIsmael) > media:
    loghelpis = str(print("\nO Consultor Ismael precisa de ajuda!",chamadosIsmael,"Chamados"))
    ishelp = 1
  

if int(chamadosKleber) > media:
    loghelpkl = str(print("\nO Consultor Kleber precisa de ajuda!",chamadosKleber,"Chamados"))
    klhelp = 1
   
   
logmedia = str(print("A média de chamados por consultor é: ",media))
logmedia = str(logmedia)


navegador.find_element_by_xpath('//*[@id="ToolBar"]/li[1]/a/img').click()
navegador.find_element_by_xpath('//*[@id="LogoutButton"]').click()

#Access Rocket Chat (internal company chat)

loadingpage = 1
while loadingpage == 1:
    time.sleep(1)
    navegador.get("https://chat.mngs.com.br/home")
    loadingpage = 0

loadingpage = 1
while loadingpage == 1:
    time.sleep(1)
    navegador.find_element_by_xpath('//*[@id="emailOrUsername"]').send_keys(#login goes here)
    loadingpage = 0
    
loadingpage = 1
while loadingpage == 1:
    time.sleep(1)
    navegador.find_element_by_xpath('//*[@id="pass"]').send_keys(#password goes here)
    loadingpage = 0

loadingpage = 1
while loadingpage == 1:
    time.sleep(1)
    navegador.find_element_by_xpath('//*[@id="login-card"]/div[2]/button[1]').click()
    loadingpage = 0

logopenticket = str(print("\n Há",chamadosAbertos,"chamados abertos na triagem desbloqueados."))
loghelpkl = str(print("\nO Consultor Kleber precisa de ajuda!",chamadosKleber,"Chamados"))

#Select Georgio to send him the tickets per consultant (Georgio is the team manager)
time.sleep(5)

navegador.get("https://chat.mngs.com.br/direct/georgio")
time.sleep(5)

time.sleep(1)
#Transforms INTS of previous variables into STR

#Tickets variables 
chamadosAbertos = str(chamadosAbertos)
chamadosDaniel = str(chamadosDaniel)
chamadosFelipe = str(chamadosFelipe)
chamadosGuilherme = str(chamadosGuilherme)
chamadosIsmael = str(chamadosIsmael)
chamadosKleber = str(chamadosKleber)

#Texts of calls and transformation to STR ----------------------------------------- --------------------------------
logopenticket = ("• Há",chamadosAbertos,"chamados abertos na triagem desbloqueados.")
logopenticket = str(logopenticket)

logmedia = ("• A média de chamados por consultor é: ",media)
logmedia = str(logmedia)

logopenticketda = ("• O Consultor Daniel tem:",chamadosDaniel,"chamados abertos.")
logopenticketda = str(logopenticketda)


logopenticketfe = ("• O Consultor Felipe tem:",chamadosFelipe,"chamados abertos.")
logopenticketfe = str(logopenticketfe)


logopenticketgu = ("• O Consultor Guilherme tem:",chamadosGuilherme,"chamados abertos.")
logopenticketgu = str(logopenticketgu)


logopenticketis = ("• O Consultor Ismael tem:",chamadosIsmael,"chamados abertos.")
logopenticketis = str(logopenticketis)


logopenticketkl = ("• O Consultor Kleber tem:",chamadosKleber,"chamados abertos.")
logopenticketkl = str(logopenticketkl)

loghelpda = ("• O Consultor Daniel precisa de ajuda!",chamadosDaniel,"Chamados")
loghelpda = str(loghelpda)

loghelpfe = ("• O Consultor Felipe precisa de ajuda!",chamadosFelipe,"Chamados")
loghelpfe = str(loghelpfe)

loghelpgu = ("• O Consultor Guilherme precisa de ajuda!",chamadosGuilherme,"Chamados")
loghelpgu = str(loghelpgu)

loghelpis = ("• O Consultor Ismael precisa de ajuda!",chamadosIsmael,"Chamados")
loghelpis = str(loghelpis)

loghelpkl = ("• O Consultor Kleber precisa de ajuda!",chamadosKleber,"Chamados")
loghelpkl = str(loghelpkl)

today = str(today)

horaatual = (" Horário atual =", current_time)
horaatual = str(horaatual)

#Messages to Georgio ------------------------------------------- ------------------------------------------------- -

#Get actual day
time.sleep(5)
navegador.find_element_by_xpath('//*[@id="chat-window-GF5D9Kvm8gm6iJK2EnwWy2n8NJJW6Dfv2B"]/div/div/footer/div/label/textarea').send_keys(today, horaatual, Keys.SHIFT, Keys.ENTER)
time.sleep(1)

#Open tickets in screening queue
navegador.find_element_by_xpath('//*[@id="chat-window-GF5D9Kvm8gm6iJK2EnwWy2n8NJJW6Dfv2B"]/div/div/footer/div/label/textarea').send_keys(logopenticket, Keys.SHIFT, Keys.ENTER)
time.sleep(1)

#Average tickets per consultant
navegador.find_element_by_xpath('//*[@id="chat-window-GF5D9Kvm8gm6iJK2EnwWy2n8NJJW6Dfv2B"]/div/div/footer/div/label/textarea').send_keys(logmedia, Keys.SHIFT, Keys.ENTER)
time.sleep(3)

if dahelp == 1:
    #If Daniel needs help
    navegador.find_element_by_xpath('//*[@id="chat-window-GF5D9Kvm8gm6iJK2EnwWy2n8NJJW6Dfv2B"]/div/div/footer/div/label/textarea').send_keys(loghelpda, Keys.SHIFT, Keys.ENTER)
    time.sleep(2)
else:
    #Daniel's open tickets
    navegador.find_element_by_xpath('//*[@id="chat-window-GF5D9Kvm8gm6iJK2EnwWy2n8NJJW6Dfv2B"]/div/div/footer/div/label/textarea').send_keys(logopenticketda, Keys.SHIFT, Keys.ENTER)
    time.sleep(3)

if fehelp == 1:
    #If Felipe needs help
    navegador.find_element_by_xpath('//*[@id="chat-window-GF5D9Kvm8gm6iJK2EnwWy2n8NJJW6Dfv2B"]/div/div/footer/div/label/textarea').send_keys(loghelpfe, Keys.SHIFT, Keys.ENTER)
    time.sleep(3)
else:
    #Felipe's open tickets
    navegador.find_element_by_xpath('//*[@id="chat-window-GF5D9Kvm8gm6iJK2EnwWy2n8NJJW6Dfv2B"]/div/div/footer/div/label/textarea').send_keys(logopenticketfe, Keys.SHIFT, Keys.ENTER)
    time.sleep(3)

if guhelp == 1:
    #If Guilherme needs help
    navegador.find_element_by_xpath('//*[@id="chat-window-GF5D9Kvm8gm6iJK2EnwWy2n8NJJW6Dfv2B"]/div/div/footer/div/label/textarea').send_keys(loghelpgu, Keys.SHIFT, Keys.ENTER)
    time.sleep(3)
else:
    #Guilherme's open tickets
    navegador.find_element_by_xpath('//*[@id="chat-window-GF5D9Kvm8gm6iJK2EnwWy2n8NJJW6Dfv2B"]/div/div/footer/div/label/textarea').send_keys(logopenticketgu, Keys.SHIFT, Keys.ENTER)
    time.sleep(3)

if ishelp == 1:
    #If Ismael needs help
    navegador.find_element_by_xpath('//*[@id="chat-window-GF5D9Kvm8gm6iJK2EnwWy2n8NJJW6Dfv2B"]/div/div/footer/div/label/textarea').send_keys(loghelpis, Keys.SHIFT, Keys.ENTER)
    time.sleep(3)
else:
    #Ismael's open tickets
    navegador.find_element_by_xpath('//*[@id="chat-window-GF5D9Kvm8gm6iJK2EnwWy2n8NJJW6Dfv2B"]/div/div/footer/div/label/textarea').send_keys(logopenticketis, Keys.SHIFT, Keys.ENTER)
    time.sleep(3)

if klhelp == 1:
    #If Kleber needs help
    navegador.find_element_by_xpath('//*[@id="chat-window-GF5D9Kvm8gm6iJK2EnwWy2n8NJJW6Dfv2B"]/div/div/footer/div/label/textarea').send_keys(loghelpkl, Keys.SHIFT, Keys.ENTER)
else:
    #Kleber's open tickets
    navegador.find_element_by_xpath('//*[@id="chat-window-GF5D9Kvm8gm6iJK2EnwWy2n8NJJW6Dfv2B"]/div/div/footer/div/label/textarea').send_keys(logopenticketkl, Keys.SHIFT, Keys.ENTER)
    time.sleep(3)


loadingpage = 1
while loadingpage == 1:
    time.sleep(1)
    navegador.find_element_by_xpath('//*[@id="chat-window-GF5D9Kvm8gm6iJK2EnwWy2n8NJJW6Dfv2B"]/div/div/footer/div/label/textarea').send_keys(Keys.ENTER)
    loadingpage = 0

#Logout Rocket
loadingpage = 1
while loadingpage == 1:
    time.sleep(1)
    navegador.find_element_by_xpath('//*[@id="rocket-chat"]/aside/header/div[1]/div[1]/img').click()
    loadingpage = 0
        
time.sleep(1)
navegador.find_element_by_xpath('/html/body/div[9]/div/div/ul[3]/li[2]').click()
loadingpage = 0

navegador.quit()