
# 🔐 Secure Encrypted Chatroom

A Python-based chatroom application that uses **Elliptic Curve Cryptography (ECC)**, **Digital Certificates**, and **Diffie-Hellman Key Exchange** to establish **end-to-end encrypted communication** between clients via a server.

---

## 🚀 Features

- ✅ **CLI and GUI clients** (PyQt5)
- 🔐 **ECC digital signatures** (custom implementation)
- 📜 **Certificate Authority (CA)** to verify identities
- 🔑 **Diffie-Hellman key exchange** to derive session keys
- 🔁 **End-to-end encrypted messaging** (XOR for simplicity)
- 🔎 **Message authenticity verification** using ECDSA
- 🌐 **Multi-client support** via threaded server

---

## 🔧 Architecture Overview

1. **Certificates**:
   - Both client and server hold a certificate signed by the local CA (`ca_private.pem`).
   - Certificates are verified using the CA's public key before communication begins.

2. **Key Exchange**:
   - Each party generates a temporary DH key.
   - Both parties derive a **shared secret** for session encryption.

3. **Message Flow**:
   - Messages are encrypted using XOR with the shared key.
   - Each message is **signed using ECDSA** and verified by the receiver.

4. **Server Role**:
   - Verifies client certificates and messages.
   - Broadcasts messages to all connected clients (with proper re-encryption).

---

## 📁 File Structure

```

project/
│
├── server.py                  # Server code
├── clientcli.py               # CLI client
├── clientgui.py               # GUI client (PyQt5)
│
├── ecc.py                     # ECC math (field, curve, signatures)
├── certificate\_authority.py   # CA, certificate signing, PEM handling
│
├── ca\_private.pem             # Certificate Authority private key
├── client\_certificate.pem     # Client certificate
├── server\_certificate.pem     # Server certificate
│
└── README.md                  # You are here

````

## 📚 Based On

Parts of the ECC code, especially the `ecc.py` file, are based on the book:  
**“Programming Bitcoin” by Jimmy Song**  
🔗 [https://github.com/jimmysong/programmingbitcoin](https://github.com/jimmysong/programmingbitcoin)

---



---

## 🛠 Requirements

- Python 3.8+
- PyQt5 (`pip install pyqt5`)

---

## 🧪 How to Run

### 1. 🔑 Generate Certificates (Optional if already present)

> If not already created:
```python
# Run manually using certificate_authority.py
from certificate_authority import CertificateAuthority, PrivateKeyWrapper

# Create CA and server cert
ca = CertificateAuthority()
ca.get_private_key_wrapper().save('ca_private.pem')

# Save server cert
server_cert = ca.sign_certificate("Server", ca.public_key)
server_cert.save('server_certificate.pem')

# Create client cert
client_cert = ca.sign_certificate("User", ca.public_key)
client_cert.save('client_certificate.pem')
````

---

### 2. ▶️ Run the Server

```bash
python server.py
```

---

### 3. 💻 Run the CLI Client

```bash
python clientcli.py
```

---

### 4. 🖥 Run the GUI Client

```bash
python clientgui.py
```

---

## 🔐 Security Notes

* **ECC + ECDSA**: Custom implementation of signing and verification (see `ecc.py`).
* **Certificates**: Manually signed by local CA (demo-style trust).
* **Key Exchange**: Uses custom Diffie-Hellman with safe prime modulus.
* **Encryption**: Simple XOR used for demo purposes. For real-world apps, use AES or ChaCha20.

---

## 🎓 Educational Value

This project is built from **scratch** to help understand:

* Elliptic Curve math
* How digital signatures work
* The role of CAs and certificates
* Key exchange protocols
* Secure socket programming in Python

---

> ⚠️ This project is a **work-in-progress prototype** intended for learning and experimentation. Not ready for production.

---

## 📜 License

MIT License

```
