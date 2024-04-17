# PRODIGY_CS_01
#Pratham Koturwar
#Caesar cipher
import tkinter as tk

def caesar_cipher(text, shift, mode):
    result = ''
    for char in text:
        if char.isalpha():  
            if mode == 'encrypt':
                shifted_char = chr((ord(char) - 65 + shift) % 26 + 65) if char.isupper() else chr((ord(char) - 97 + shift) % 26 + 97)
            elif mode == 'decrypt':
                shifted_char = chr((ord(char) - 65 - shift) % 26 + 65) if char.isupper() else chr((ord(char) - 97 - shift) % 26 + 97)
            else:
                raise ValueError("Mode must be 'encrypt' or 'decrypt'")
            result += shifted_char
        else:
            result += char 
    return result

def encrypt_decrypt():
    mode = mode_var.get()
    message = message_entry.get()
    shift = int(shift_entry.get())
    
    if mode == 'encrypt':
        result_label.config(text="Encrypted message: " + caesar_cipher(message, shift, mode))
    elif mode == 'decrypt':
        result_label.config(text="Decrypted message: " + caesar_cipher(message, shift, mode))

# Tkinter GUI window
root = tk.Tk()
root.title("Caesar Cipher")

# buttons
mode_var = tk.StringVar()
mode_var.set("encrypt")
encrypt_radio = tk.Radiobutton(root, text="Encrypt", variable=mode_var, value="encrypt")
decrypt_radio = tk.Radiobutton(root, text="Decrypt", variable=mode_var, value="decrypt")
encrypt_radio.grid(row=0, column=0)
decrypt_radio.grid(row=0, column=1)

# message entry field
message_label = tk.Label(root, text="Message:")
message_label.grid(row=1, column=0, sticky="w")
message_entry = tk.Entry(root, width=40)
message_entry.grid(row=1, column=1, columnspan=2)

# shift entry field
shift_label = tk.Label(root, text="Shift:")
shift_label.grid(row=2, column=0, sticky="w")
shift_entry = tk.Entry(root, width=10)
shift_entry.grid(row=2, column=1)

# button to perform encryption/decryption
encrypt_button = tk.Button(root, text="Encrypt/Decrypt", command=encrypt_decrypt)
encrypt_button.grid(row=3, column=0, columnspan=2)

# label to display result
result_label = tk.Label(root, text="")
result_label.grid(row=4, column=0, columnspan=2)

# Run the Tkinter event loop
root.mainloop()
