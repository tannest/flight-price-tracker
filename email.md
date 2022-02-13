#Sending HTML Email
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from email.mime.application import MIMEApplication
import smtplib, ssl


#secure username/password from .env
load_dotenv()
passwordfunction = (os.environ.get('email_password'))
password = (str(passwordfunction))


smtp_server = 'smtp.office365.com'
smtp_port = 587
#Replace with your own gmail account
user = 'FULLEMAIL ADDRESS'
#recipient at top
message = MIMEMultipart('mixed')
message['From'] = 'Contact <{sender}>'.format(sender = user)
message['To'] = recipient
#message['cc'] = 
message['Subject'] = SUBJECT TITLE HERE

msg_content = (f'''
<!DOCTYPE html>
<html>
    <body>
   
</body>
    <footer>
   
    </footer>
</html>
''')
body = MIMEText(msg_content, 'html')
message.attach(body)

#IF attachment to be added
attachmentPath = "C:\\Users\\cpillsbury\\Downloads\\DoS-Host-Alert-" + str(linknumber) + "-.pdf"
try:
   with open(attachmentPath, "rb") as attachment:
      p = MIMEApplication(attachment.read(),_subtype="pdf")
      p.add_header('Content-Disposition', "attachment; filename= %s" % attachmentPath.split("\\")[-1])
      message.attach(p)
except Exception as e:
   print(str(e))

msg_full = message.as_string()
context = ssl.create_default_context()

with smtplib.SMTP(smtp_server, smtp_port) as server:
   server.ehlo()
   server.starttls(context=context)
   server.ehlo()
   server.login(user, password)
   server.sendmail(user, recipient, msg_full)
   server.quit()