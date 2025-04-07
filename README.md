import smtplib
import time
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart

to = 'TARGET@gmail.com'
froma = 'ATTACKER@gmail.com'


message = MIMEMultipart()
message['From'] = froma
message['To'] = to
message['Subject'] = 'TITLE'

body = 'MESSAGE'
message.attach(MIMEText(body, 'plain', 'utf-8'))  


with smtplib.SMTP('smtp.gmail.com', 587) as smtpserver:
    smtpserver.ehlo()
    smtpserver.starttls()
    smtpserver.ehlo()
    smtpserver.login('ATTACKER@gmail.com', 'KEY FROM APP PASSWORD IN UR GMAIL ACCOUNT')
    
    for i in range(5): #CHANGE THE NUMBER TO INCREASE OR DECREASE THE SENDING AMOUNT
        smtpserver.sendmail(froma, to, message.as_string())  
        print(f"Email {i+1} sent.")
        time.sleep(1)

