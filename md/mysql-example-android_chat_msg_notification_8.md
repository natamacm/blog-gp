---
title: mysql example android chat msg notification 8 (snippet)
date: 2020-03-03
tags: ["python"]
---
Python mysql example 'android chat msg notification 8'

Functions in program: 
* `def send_email(subject, body, email):`
* `def login(msg_received):`
* `def send_verification_code(firstname, lastname, username, email):`
* `def decrypt_text(text_to_decrypt):`
* `def encrypt_text(text_to_encrypt):`
* `def check_new_messages(msg_received):`
* `def receive_messages(msg_received):`
* `def receive_chats(msg_received):`
* `def send(msg_received):`
* `def verify_code(email, verification_code):`
* `def verify(msg_received):`
* `def register(msg_received):`
* `def chat():`

Modules used in program: 
* `import cryptography.fernet`
* `import smtplib, ssl`
* `import json`
* `import sys`
* `import mysql.connector`
* `import flask`

## python android chat msg notification 8

Python mysql example: android chat msg notification 8

```python
import flask
import mysql.connector
import sys
import json
import smtplib, ssl
from email.mime.text import MIMEText
import cryptography.fernet

app = flask.Flask(__name__)

@app.route('/', methods = ['GET', 'POST'])
def chat():
    msg_received = flask.request.get_json()
    msg_subject = msg_received["subject"]

    if msg_subject == "register":
        return register(msg_received)
    elif msg_subject == "login":
        return login(msg_received)
    elif msg_subject == "verify":
        return verify(msg_received)
    elif msg_subject == "send":
        return send(msg_received)
    elif msg_subject == "receive_chats":
        return receive_chats(msg_received)
    elif msg_subject == "receive_messages":
        return receive_messages(msg_received)
    elif msg_subject == "check_new_messages":
        return check_new_messages(msg_received)
    else:
        return "Invalid request."

def register(msg_received):
    first_name = msg_received["first_name"]
    lastname = msg_received["last_name"]
    username = msg_received["username"]
    email = msg_received["email"]

    select_query = "SELECT * FROM users where username = " + "'" + username + "'"
    db_cursor.execute(select_query)
    records = db_cursor.fetchall()
    if len(records) != 0:
        return "username" # "Username already exists. Please chose another username."

    select_query = "SELECT * FROM users where email = " + "'" + email + "'"
    db_cursor.execute(select_query)
    records = db_cursor.fetchall()
    if len(records) != 0:
        return "email" # "E-mail is already registered."

    send_verification_code(first_name, lastname, username, email) # Encrypt e-mail using 2 keys and send the code to the user e-mail.

    return "success"

def verify(msg_received):
    firstname = msg_received["firstname"]
    lastname = msg_received["lastname"]
    username = msg_received["username"]
    email = msg_received["email"]
    password = msg_received["password"]
    verification_code = msg_received["verification_code"]

    select_query = "SELECT * FROM users where username = " + "'" + username + "'"
    db_cursor.execute(select_query)
    records = db_cursor.fetchall()
    if len(records) != 0:
        return "Another user just used the username. Please chose another username."

    select_query = "SELECT * FROM users where email = " + "'" + email + "'"
    db_cursor.execute(select_query)
    records = db_cursor.fetchall()
    if len(records) != 0:
        return "Another user just registered using the e-mail entered."

    verification_state = verify_code(email, verification_code)

    if verification_state == True:
        insert_query = "INSERT INTO users (first_name, last_name, username, email, password, email_confirmed) VALUES (%s, %s, %s, %s, MD5(%s), %s)"
        insert_values = (firstname, lastname, username, email, password, True)
        try:
            db_cursor.execute(insert_query, insert_values)
            chat_db.commit()
            print("This e-mail", email, " is verified and user is registered successfully.")
            subject = "Welcome to HiAi"
            body = "Hi " + firstname + " " + lastname + ",\n\nYour account is created successfully at HiAi. You can login with your username and password into the Android app to send and receive messages. \n\nYour username is " + username + "\n\nIf you forgot your password, just contact ahmedgad@hiai.website for resetting it. \n\nGood luck.\nHiAi Team\nahmedgad@hiai.website"
            send_email(subject, body, email)
            return "success"
        except Exception as e:
            print("Error while inserting the new record :", repr(e))
            return "Error while processing the request."
    else:
        print("This e-mail", email, " verification failed.")
        return "failure"

def verify_code(email, verification_code):
    decoded_email = decrypt_text(verification_code)

    if decoded_email == email:
        return True # Email verification succeeded.
    else:
        return False # Email verification failed.

def send(msg_received):
    text_msg = msg_received["msg"]
    sender_username = msg_received["sender_username"]

    receiver_username = msg_received["receiver_username"]

    select_query = "SELECT * FROM users where username = " + "'" + receiver_username + "'"
    db_cursor.execute(select_query)
    records = db_cursor.fetchall()
    if len(records) == 0:
        return "Invalid receiver username."

    select_query = "SELECT * FROM users where username = " + "'" + sender_username + "'"
    db_cursor.execute(select_query)
    records = db_cursor.fetchall()
    if len(records) == 0:
        return "Invalid sender username."

    insert_query = "INSERT INTO messages (sender_username, receiver_username, message) VALUES (%s, %s, %s)"
    insert_values = (sender_username, receiver_username, text_msg)

    try:
        db_cursor.execute(insert_query, insert_values)
        chat_db.commit()
        print(db_cursor.rowcount, "New record inserted successfully.")
    except Exception as e:
        print("Error while inserting the new record :", repr(e))
        return "Error while processing the request."

    update_query = "UPDATE users SET notified_by_new_messages = false WHERE username = " + "'" + receiver_username + "'"
    db_cursor.execute(update_query)
    chat_db.commit()    

    print("Received message from :", sender_username, "(", text_msg, ") to be sent to ", receiver_username)
    return "success"

def receive_chats(msg_received):
    receiver_username = msg_received["receiver_username"]
    receiver_username = decrypt_text(receiver_username)

    select_query = "SELECT first_name, last_name FROM users where username = " + "'" + receiver_username + "'"
    db_cursor.execute(select_query)
    records = db_cursor.fetchall()
    if len(records) == 0:
        return "Invalid receiver username."

    select_query = "SELECT DISTINCT sender_username FROM messages where receiver_username = " + "'" + receiver_username + "'"
    db_cursor.execute(select_query)
    records = db_cursor.fetchall()
    if len(records) == 0:
        print("No messages delivered for username " + receiver_username)
        return "0"

    update_query = "UPDATE users SET notified_by_new_messages = true, last_date_conversations_fetched = CURRENT_TIMESTAMP WHERE username = " + "'" + receiver_username + "'"
    db_cursor.execute(update_query)
    chat_db.commit()

    all_chats = {}
    for record_idx in range(len(records)):
        curr_record = records[record_idx]
        sender_username = curr_record[0]
        
        curr_chat = {}
        curr_chat["username"] = sender_username 
        curr_chat["message"] = "MESSAGE"
        curr_chat["date"] = "DATE"

        all_chats[str(record_idx)] = curr_chat

    all_chats = json.dumps(all_chats)
    print("Sending Chat(s) :", all_chats)
    return all_chats

def receive_messages(msg_received):
    receiver_username = msg_received["receiver_username"]

    sender_username = msg_received["sender_username"]

    select_query = "SELECT * FROM users where username = " + "'" + receiver_username + "'"
    db_cursor.execute(select_query)
    records = db_cursor.fetchall()
    if len(records) == 0:
        return "Invalid receiver username."

    select_query = "SELECT message, receive_date, sender_username FROM messages where (receiver_username = " + "'" + receiver_username + "' AND sender_username = " + "'" + sender_username + "') OR (receiver_username = " + "'" + sender_username + "' AND sender_username = " + "'" + receiver_username + "') ORDER BY receive_date DESC"
    db_cursor.execute(select_query)
    records = db_cursor.fetchall()
    if len(records) == 0:
        print("No messages delivered for username " + receiver_username)
        return "0"

    all_messages = {}
    for record_idx in range(len(records)):
        curr_record = records[record_idx]
        message = curr_record[0]
        receiveDate = curr_record[1]
        sender_username = curr_record[2]

        curr_message = {}
        curr_message["message"] = message
        curr_message["date"] = str(receiveDate)
        curr_message["sender_username"] = sender_username

        all_messages[str(record_idx)] = curr_message

    all_messages = json.dumps(all_messages)
    print("Sending message(s) :", all_messages)
    return all_messages

def check_new_messages(msg_received):
    receiver_username = msg_received["receiver_username"]

    select_query = "SELECT last_date_conversations_fetched FROM users WHERE username = " + "'" + receiver_username + "' AND notified_by_new_messages = false"
    db_cursor.execute(select_query)
    records = db_cursor.fetchall()

    reply_json = {}
    if len(records) == 0:
        reply_json["num_messages"] = "0" # 0 means no new messages for the username
        reply_json["senders"] = ""
        reply_json = json.dumps(reply_json)
        return reply_json
    
    last_date_conversations_fetched = str(records[0][0])

    update_query = "UPDATE users SET notified_by_new_messages = true WHERE username = " + "'" + receiver_username + "'"
    db_cursor.execute(update_query)
    chat_db.commit()

    select_query = "SELECT sender_username FROM messages WHERE receiver_username = " + "'" + receiver_username + "' AND receive_date > " + "'" + last_date_conversations_fetched + "'"
    db_cursor.execute(select_query)
    records = db_cursor.fetchall()

    if len(records) == 0:
        reply_json["num_messages"] = "0" # 0 means no new messages for the username
        reply_json["senders"] = ""
        reply_json = json.dumps(reply_json)
        return reply_json
    else:
        select_query = "SELECT DISTINCT sender_username FROM messages WHERE receiver_username = " + "'" + receiver_username + "' and receive_date > " + "'" + last_date_conversations_fetched + "'"
        db_cursor.execute(select_query)
        records_usernames = db_cursor.fetchall()

        reply_json["num_messages"] = str(len(records)) # returns the number of new messages sent to the username
        if len(records_usernames) == 1:
            reply_json["senders"] = records_usernames[0][0]
        elif len(records_usernames) == 2:
            reply_json["senders"] = records_usernames[0][0] + " and " + records_usernames[1][0]
        else:
            reply_json["senders"] = records_usernames[0][0] + ", " + records_usernames[1][0] + ", and " + str(len(records_usernames)-2) + " more"
        reply_json = json.dumps(reply_json)
        return reply_json

def encrypt_text(text_to_encrypt):
    key_file1 = open("encryption_key1.key", "rb")
    encryption_key1 = key_file1.read()
    key_file1.close()
    
    key_file2 = open("encryption_key2.key", "rb")
    encryption_key2 = key_file2.read()
    key_file2.close()

    encoded_email = text_to_encrypt.encode()

    f = cryptography.fernet.MultiFernet([cryptography.fernet.Fernet(encryption_key1), cryptography.fernet.Fernet(encryption_key2)])
    
    encrypted_text = f.encrypt(encoded_email)
    
    return encrypted_text

def decrypt_text(text_to_decrypt):
    key_file1 = open("encryption_key1.key", "rb")
    encryption_key1 = key_file1.read()
    key_file1.close()
    
    key_file2 = open("encryption_key2.key", "rb")
    encryption_key2 = key_file2.read()
    key_file2.close()
    
    f = cryptography.fernet.MultiFernet([cryptography.fernet.Fernet(encryption_key1), cryptography.fernet.Fernet(encryption_key2)])

    try:
        decrypted_text = f.decrypt(text_to_decrypt.encode('utf-8'))
    except:
        return False # Email verification failed.

    decoded_text = decrypted_text.decode()

    return decoded_text

def send_verification_code(firstname, lastname, username, email):
    
    encrypted_email = encrypt_text(email)
    
    body = "Hi " + firstname + " " + lastname + ",\n\nThanks for registering for HiAi Chat System.\n\nYour username is " + username + ".\nTo verify your account, just copy the verification code found below, return back to the Android app, paste the code, and finally click the Verify button.\n\n\n" + encrypted_email.decode()
    subject = "HiAi Verification"

    send_email(subject, body, email)

def login(msg_received):
    username = msg_received["username"]
    password = msg_received["password"]

    select_query = "SELECT first_name, last_name FROM users where username = " + "'" + username + "' and password = " + "MD5('" + password + "')"
    db_cursor.execute(select_query)
    records = db_cursor.fetchall()

    if len(records) == 0:
        return "failure"
    else:
        return "success"

def send_email(subject, body, email):
    port = 465  # For SSL
#    smtp_server = "smtp.gmail.com"
    smtp_server = "hiai.website"
    sender_email = "ahmedgad@hiai.website"  # Enter your address
#    sender_email = "afgfcit@gmail.com"  # Enter your address
    password = "..."

    msg_body = body
    
    msg = MIMEText(msg_body, 'plain', 'utf-8')

    # add in the actual person name to the message template
    msg['From'] = sender_email
    msg['To'] = email
    msg['Subject'] = subject

    context = ssl.create_default_context()
    with smtplib.SMTP_SSL(smtp_server, port, context=context) as server:
        server.login(sender_email, password)
        server.sendmail(sender_email, email, msg.as_string())

try:
    chat_db = mysql.connector.connect(host="localhost", user="root", passwd="ahmedgad", database="chat_db")
except:
    sys.exit("Error connecting to the database. Please check your inputs.")

db_cursor = chat_db.cursor()

app.run(host="0.0.0.0", port=5000, debug=True, threaded=True)

```

## Python links

- Learn Python: https://pythonbasics.org/
- Python Tutorial: https://pythonprogramminglanguage.com
