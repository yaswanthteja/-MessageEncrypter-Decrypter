
#   Message Encryption-Decryption

Encryption is the process that transforms the text or information to the unrecognizable form and decryption is the process to convert the encrypted message into original form.


Message encoding and decoding is the process to first convert the original text to the random and meaningless text called ciphertext. This process is called encoding. Decoding is the process to convert that ciphertext to the original text. This process is also called the Encryption-Decryption process.
 Click on the link below to view the blog post

 # [BLOG LINK](https://dev.to/yaswanthteja/message-encryption-decryption-using-python-j5l)


#   Prerequisites

 Tkinter, and base64 library.
 - Tkinter is a standard GUI python library
- base64 module provides a function to encode the binary data to ASCII characters and decode that ASCII characters back to binary data.
To install the library we use pip install command on the command prompt

```
pip install tkinter
pip install base64

```



## Project File Structure  

- Import module
- Create display window
- Define function
- Define labels and buttons

## Import Libraries
```bash
from tkinter import *
import base64
```
The first step is to import tkinter and base64 libraries.

## Initialize Window

```bash
root = Tk()

root.geometry('500x300')
root.resizable(0,0)
root.title(" Message encrypt and decrypt")

```
- Tk() initialized tkinter which means window created
- geometry() set the width and height of the window
- resizable(0,0) set the fixed size of the window
- title() set the title of the window
 
 
 
Label() widget use to display one or more than one line of text that users aren’t able to modify.
 

```bash
Label(root, text ='ENCRYPT DECRYPT', font = 'arial 20 bold').pack()

Label(root, text ='YOUR DATA', font = 'arial 20 bold').pack(side =BOTTOM)
```


## Define variables
```bash
Text = StringVar()
private_key = StringVar()
mode = StringVar()
Result = StringVar()
```
- Text variable stores the message to encode and decode
- private_key variable store the private key used to encode and decode
- mode is used to select that is either encoding or decoding
 - Result store the result

## Function to encrypt


```bash
def Encode(key,message):
    enc=[]

    for i in range(len(message)):
        key_c = key[i % len(key)]
         enc.append(chr((ord(message[i]) + ord(key_c)) % 256))
    return base64.urlsafe_b64encode("".join(enc).encode()).decode()
```

### Encode function have arguments – key and message
- enc = [] is an empty list
- We run loop till the length of the message
- i% of len(key) gives the remainder of division between i and len(key) and that remainder used as an index of key the value of key at that index is stored in key_c
- ord() function takes string argument of a single unicode character and return its integer unicode value
- chr() function takes an integer argument and returns the string.
- ord (message[i]) convert the value of message at index i into the integer value
- ord(key_c) converts the key_c value to integer value
- ord(message[i]) + ord(key_c)) % 256 gives the remainder of division of addition of ord(message[i]) and ord( key_c) with 256 and passes that remainder to chr() function
- chr() function converts that integer value to string and store to enc
- base64.urlsafe_b64encode encode a string.
- The join() method joins each element of list, string, and tuple by a string separator and returns the concatenated string.
- encode() method returns utf-8 encoded message of the string.
- decode() method decodes the string.
- return gives the result of the encoded string.

##  Function to decode




```bash
def Decode(key,message):
    dec=[]
    message = base64.urlsafe_b64decode(message).decode()

    for i in range(len(message)):
        key_c = key[i % len(key)]
        dec.append(chr((256 + ord(message[i])- ord(key_c)) % 256))
    return "".join(dec)

```


## Decode() function has arguments – key, message
- dec=[] is an empty list
- Decode the content from input and write the result in binary to the output
- We ran the loop till the length of the message
- 256 + ord(message[i]) – ord(key_c)) % 256 gives the remainder of addition of 256 with subtraction of ord(message[i]) – ord( key_c) and then division with 256 and passes that remainder to chr() function
- chr() function convert integer value to string and store to dec
- return “”.join(dec) return the result

## Function to set mode


```bash

def Mode():
    if(mode.get() == 'e'):
        Result.set(Encode(private_key.get(), Text.get()))
    elif(mode.get() == 'd'):
        Result.set(Decode(private_key.get(), Text.get()))
    else:
        Result.set('Invalid Mode')

```
- If the mode set by the user is ‘e’ then the Encode() function will be called
- If the mode set to ‘d‘ then the Decode() function will be called
- Else print ‘invalid mode’
- private_key.get() and Text.get() values are pass to the arguments of Encode() and Decode() function

 

## Function to exit window
```
def Exit():
    root.destroy()

```
- root.destroy() will quit the program by stopping the mainloop()

## Function to reset window


```bash
def Reset():
    Text.set("")
    private_key.set("")
    mode.set("")
    Result.set("")         

```
This function set all variables to empty string
## Labels and Buttons
```
Label(root, font= 'arial 12 bold', text='MESSAGE').place(x= 60,y=60)
Entry(root, font = 'arial 10', textvariable = Text, bg = 'ghost white').place(x=290, y = 60)

Label(root, font = 'arial 12 bold', text ='KEY').place(x=60, y = 90)
Entry(root, font = 'arial 10', textvariable = private_key , bg ='ghost white').place(x=290, y = 90)

Label(root, font = 'arial 12 bold', text ='MODE(e-encode, d-decode)').place(x=60, y = 120)
Entry(root, font = 'arial 10', textvariable = mode , bg= 'ghost white').place(x=290, y = 120)
Entry(root, font = 'arial 10 bold', textvariable = Result, bg ='ghost white').place(x=290, y = 150)

Button(root, font = 'arial 10 bold', text = 'RESULT'  ,padx =2,bg ='LightGray' ,command = Mode).place(x=60, y = 150)

Button(root, font = 'arial 10 bold' ,text ='RESET' ,width =6, command = Reset,bg = 'LimeGreen', padx=2).place(x=80, y = 190)

Button(root, font = 'arial 10 bold',text= 'EXIT' , width = 6, command = Exit,bg = 'OrangeRed', padx=2, pady=2).place(x=180, y = 190)

root.mainloop()
```
- Label() widget use to display one or more than one line of text that users aren’t able to modify.
- Entry() widget used to create an input text field.
- Button() widget used to display button on our window
- root is the name which we refer to our window
- text which we display on the label
- font in which the text is written
- insertwidth use to set the width of the insertion cursor
- bg sets the background colour
- command is call when the button is click
- textvariable used to retrieve the current text to the entry widget
- root.mainloop() is a method that executes when we want to run our program.
##  output

basic window 

![window](https://github.com/yaswanthteja/-MessageEncrypter-Decrypter/blob/main/window.png)

Encryption
![Encrypt](https://github.com/yaswanthteja/-MessageEncrypter-Decrypter/blob/main/Encrypt.png)

Decryption
![Decryption](https://github.com/yaswanthteja/-MessageEncrypter-Decrypter/blob/main/Decrypt.png)
