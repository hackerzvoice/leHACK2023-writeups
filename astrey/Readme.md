# Astray

## Description
Nairobi has figured out a quicker way to print the notes. But she’s unable to access the computer which has the controls. Get her a key, and she will reward you!


## Challenge

We've given an image contains masked RSA private key and a target SSH service.

![](assets/key.png)

Goal is very clear where we've to recover private key and login to SSH service to get flag. This challenge is inspired from [CryptoHack](https://blog.cryptohack.org/twitter-secrets). We follow the blogpost and can try to solve this challenge. Let's extract the text from the image using a python ocr.

```python
import pytesseract
pytesseract.image_to_string('key.png')

"""
'MITIKATBAAKCAgEAQN6QL9+vpOIkMWms leoQ4WluAs fEjup9520S53aPQj/zIUb1+\ncaAWGWffXsjDk9+G94RpI xUsab2EhkdqU6p+wS4GHkLaROULOFmc7MirCyrf1FxF+\n4aEoAGiyyg8h1H1/9q1mkY3dGSwiKkP93E3mF qop@xTsYNWPv@bc9BufpeZKkFQov\ng4a4rdLt¥AJqJa7C4vo8MagAaxZMCoVPeQrD1uwY1DTGM2+uPr7w3Caghw7onU67\no6umEyVeY+nM36spAbBBNFhc9UpMagvk@Eghqw3yTbp3sOUbXyq7ir3FAtYxksla\nc/D7VMk6yolkt4vDHTFohy1EmiY aA4MyOKs5LnMBBEDXPI6b/ aQhAyy@2r+eqTn7\n\n \n\nQ39sjQ2TA/RAGQKCAQEAXp3XCBH1098nqAcLVyde34LuduloWv927qqnZxXx4pCS8\n/YwdHbZ/kuFjdqvmrez51G9ABcNt2yYXau95ag6EcpTsB@8HDerGe9XmilA57mvr:\nbKqp633nM6RdaT29mkDkbPNORLGcDXvxwxofHztOGsdEQYTmbQSKLS7eVeTF+uY4.\nUbLJiWnEOixw/IvZFUkIFVrws@GqCO/Y7pnxY19eAu5XYMAuuucXGEHSZhbKmF rU\nnbgX3pWCAqVoP1U2MO9SNRmi+iRtNrSRvOsF9MUF9Qqo8LDqlxst28BT79pdiimSh\nU5t3P7ze9FQVi3306YiqDGBOCBgQNRPNScHilinHMwKCAQA8dHdngé8afptKInZi\n366a0gp/AHU3nxpadKMwi FY5kKUHM1PM84+zdnHLTuUgom6jtkZ@o010014dA88KM\nNBrbxLA6wD4stwxxHJAV4Nrt@287+f 1WhATQTgYwocsnOcC+/kLTT+@ZGIIFNUOM\nilvD1x/Yme+ZeABTod5VpkjuheV2gI zW4eI5gTN4tbLVTdJ9ySqDZVWUCpzBOXLm\nUiT/hpZ+j1DBs2U0K2ZgF eHyT1YCj6i@QUIV+uSDDQa/6trajLvIKdTpX3BSNEvi\nb061/sLNtt1j aOXV5ykZRtplé6rvRzhzg7gErkNdXxtoGz9b2KEMn19w9ZiRwCdaG+\n+Gm5A01BAGaGd8ecrYS5ntjnutz1PtXJ2prddi7zDEurH/rgppbkuAIR373EXxRnm\n\nsae END RSA PRIVATE KEY----~-\n\x0c'
"""
```

We replace new lines and format it better.

```
-----BEGIN RSA PRIVATE KEY-----
MITIKATBAAKCAgEAQN6QL9+vpOIkMWmsleoQ4WluAsfEjup9520S53aPQj/zIUb1+
caAWGWffXsjDk9+G94RpIxUsab2EhkdqU6p+wS4GHkLaROULOFmc7MirCyrf1FxF+
4aEoAGiyyg8h1H1/9q1mkY3dGSwiKkP93E3mFqop@xTsYNWPv@bc9BufpeZKkFQov
g4a4rdLt¥AJqJa7C4vo8MagAaxZMCoVPeQrD1uwY1DTGM2+uPr7w3Caghw7onU67
o6umEyVeY+nM36spAbBBNFhc9UpMagvk@Eghqw3yTbp3sOUbXyq7ir3FAtYxksla
c/D7VMk6yolkt4vDHTFohy1EmiYaA4MyOKs5LnMBBEDXPI6b/aQhAyy@2r+eqTn7


Q39sjQ2TA/RAGQKCAQEAXp3XCBH1098nqAcLVyde34LuduloWv927qqnZxXx4pCS8
/YwdHbZ/kuFjdqvmrez51G9ABcNt2yYXau95ag6EcpTsB@8HDerGe9XmilA57mvr:
bKqp633nM6RdaT29mkDkbPNORLGcDXvxwxofHztOGsdEQYTmbQSKLS7eVeTF+uY4.
UbLJiWnEOixw/IvZFUkIFVrws@GqCO/Y7pnxY19eAu5XYMAuuucXGEHSZhbKmFrU
nbgX3pWCAqVoP1U2MO9SNRmi+iRtNrSRvOsF9MUF9Qqo8LDqlxst28BT79pdiimSh
U5t3P7ze9FQVi3306YiqDGBOCBgQNRPNScHilinHMwKCAQA8dHdngé8afptKInZi
366a0gp/AHU3nxpadKMwiFY5kKUHM1PM84+zdnHLTuUgom6jtkZ@o010014dA88KM
NBrbxLA6wD4stwxxHJAV4Nrt@287+f1WhATQTgYwocsnOcC+/kLTT+@ZGIIFNUOM
ilvD1x/Yme+ZeABTod5VpkjuheV2gIzW4eI5gTN4tbLVTdJ9ySqDZVWUCpzBOXLm
UiT/hpZ+j1DBs2U0K2ZgF eHyT1YCj6i@QUIV+uSDDQa/6trajLvIKdTpX3BSNEvi
b061/sLNtt1j aOXV5ykZRtplé6rvRzhzg7gErkNdXxtoGz9b2KEMn19w9ZiRwCdaG+
+Gm5A01BAGaGd8ecrYS5ntjnutz1PtXJ2prddi7zDEurH/rgppbkuAIR373EXxRnm

-----END RSA PRIVATE KEY-----
```

It still have some issues. Let's fix text by looking at image.

```
-----BEGIN RSA PRIVATE KEY-----
MIIJKAIBAAKCAgEAqN6QL9+vpOIkMWms1eoQ4WuAsfEjup9520S53aPQj/zJUb1+
caAwGWffXsjDk9+G94RpJxUsab2EhkdqU6p+wS4GHkLaROU1OFmc7MrCyrf1fxf+
4aEoAGiyyg8hlHl/9q1mkY3dGSwWKP9jE3mFqOp0xTsYNWPv0bc9Bufp0ZKkfQov
g4a4rdLtfAJqJa7C4vo8MagAaxZMCoVPeQrD1uwY1DTGM2+uPr7w3Caghw7onU67
o6umEyVeY+nM36spAbBBNFhc9UpMagvk0Eghqw3yTbp3sOUbXyq7ir3FAtYxksla
c/D7VMk6yolKt4vDHTFohy1EmiYaA4MyOKs5LnMBBEpXPJ6b/aQhAyy02r+EjTn7


Q39sjQ2TA/RAqQKCAQEAxp3XCBH1Q98nqAcLVydc34Ludu1oWv927qqnZxX4pCS8
/YwdHbZ/kuFjdqvmrez5lG9ABcNt2yYXau95ag6EcpTsB08HDerG09XmilA57mvr
bKqp633nM6RdaT29mkDkbPNORLGcDXvxwxofHztOGsdEQYTmbQSKLS7eVeTf+uY4
UbLJiWnEOixw/IvZfUkJfVrws0GqCO/Y7pnXYl9eAu5XYMAuuucXGEH5ZhbKmFrU
nbgX3pWCAqVoP1U2MO95NRmi+iRtNr5RvOsF9MuF9Qqo8LDqlxst28BT79pdWm5h
U5t3P7ze9fQVi33o6YiqDGB0CBgQNRPnScHi1inHMwKCAQA8dHdnq68afptKlnZi
J66aOqp/AHU3nxpadKMwifY5kUHM1PM84+zdnHLTuUgom6jtkZ0oOIoO14dA88KM
NBrbxLA6wD4stwxxHJAv4Nrt0287+f1WhATQTgYwocsnOcC+/kLTT+0ZGJJFnUOM
ilvD1x/Ymc+ZeABTod5VpkjuheV2gIzW4eI5gTN4tbLVTdJ9ySqDZVWUCpzBOXLm
UiT/hpZ+j1DBs2UOK2ZgFeHyTlYCj6i0QUJV+uSDDQa/6trajLvJKdTpX3BSNEvi
bO6l/sLNtt1jaOXV5ykZRtpl6rvRzhzg7qErkNdXtoGz9b2KEMnl9w9ZiRwCdaG+
+Gm5AoIBAGaGd8ecrYS5ntjnufzlPtXJ2prddi7zDEurH/rgppbkuAIR373ExRnm

-----END RSA PRIVATE KEY-----
```

For next part we can use [Cyberchef](https://gchq.github.io/CyberChef/). Select From Base64 and To Hex recipies. Paste the key contents . We can get the required info from the data.

```python
N_upper_bits = 0xa8de902fdfafa4e2243169acd5ea10e16b80b1f123ba9f79db44b9dda3d08ffcc951bd7e71a0301967df5ec8c393df86f7846927152c69bd8486476a53aa7ec12e061e42da44e53538599ceccac2cab7f57f17fee1a1280068b2ca0f2194797ff6ad66918ddd192c1628ff63137985a8ea74c53b183563efd1b73d06e7e9d192a47d0a2f8386b8add2ed7c026a25aec2e2fa3c31a8006b164c0a854f790ac3d6ec18d434c6336fae3ebef0dc26a0870ee89d4ebba3aba613255e63e9ccdfab2901b04134585cf54a4c6a0be4d04821ab0df24dba77b0e51b5f2abb8abdc502d63192c95a73f0fb54c93aca894ab78bc31d3168872d449a261a03833238ab392e7301044a573c9e9bfda421032cb4dabf848d39fb
p_lower_bits = 0x437f6c8d0d9303f440a9
q = 0xc69dd70811f543df27a8070b57275cdf82ee76ed685aff76eeaaa76715f8a424bcfd8c1d1db67f92e16376abe6adecf9946f4005c36ddb26176aef796a0e847294ec074f070deac6d3d5e68a5039ee6beb6caaa9eb7de733a45d693dbd9a40e46cf34e44b19c0d7bf1c31a1f1f3b4e1ac7444184e66d048a2d2ede55e4dffae63851b2c98969c43a2c70fc8bd97d49097d5af0b341aa08efd8ee99d7625f5e02ee5760c02ebae7171841f96616ca985ad49db817de958202a5683f553630ef793519a2fa246d36be51bceb05f4cb85f50aa8f0b0ea971b2ddbc053efda5d5a6e61539b773fbcdef5f4158b7de8e988aa0c60740818103513e749c1e2d629c733
dp = 0x3c747767abaf1a7e9b4a96766227ae9a3aaa7f0075379f1a5a74a33089f6399141ccd4f33ce3ecdd9c72d3b948289ba8ed919d28388a0ed78740f3c28c341adbc4b03ac03e2cb70c711c902fe0daedd36f3bf9fd568404d04e0630a1cb2739c0befe42d34fed191892459d438c8a5bc3d71fd899cf99780053a1de55a648ee85e576808cd6e1e239813378b5b2d54dd27dc92a836555940a9cc13972e65224ff86967e8f50c1b3650e2b666015e1f24e56028fa8b4414255fae4830d06bfeadada8cbbc929d4e95f7052344be26ceea5fec2cdb6dd6368e5d5e7291946da65eabbd1ce1ce0eea12b90d757b681b3f5bd8a10c9e5f70f59891c0275a1bef869b9
dq_upper_bits = 0x668677c79cad84b99ed8e7b9fce53ed5c9da9add762ef30c4bab1ffae0a696e4b80211dfbdc4c519e6
e = 65537
p = 0xd9a88ceb5b19d65e1c57467c8726fb1e619564a37a825fcd0e2d0e09b857b1afbe7e3076d5d6ee499239bf64ae0589dbee172fe260b49170aa3b9675a7dbc2497d7623fb3b3c406d793347b772473a4c7e2ba47e12c7aa7106e9858173db38ea410b58c7112639a7fb22f83d3af076c8ba7aa8b3cac5ecfbad649fecb6a3670712e49e4a71de841ae1adb2cea4f3c282d07233657783226a95d4db0e7f10bd7d0fd99826ce53d972bd297b343ffd6a39f983e5e339816f8e53b6abe83acc978841063c2273529cd07255098ce9dc7d8b7d1b6aaaf90ad8d9b01ac3598ad8732b36baa6bf72d9c331117006452f4d70c4e34cff6f1a1b437f6c8d0d9303f440a9
```

The key can be extracted with below script.

```python
from Crypto.Util.number import isPrime

N_upper_bits = 0xa8de902fdfafa4e2243169acd5ea10e16b80b1f123ba9f79db44b9dda3d08ffcc951bd7e71a0301967df5ec8c393df86f7846927152c69bd8486476a53aa7ec12e061e42da44e53538599ceccac2cab7f57f17fee1a1280068b2ca0f2194797ff6ad66918ddd192c1628ff63137985a8ea74c53b183563efd1b73d06e7e9d192a47d0a2f8386b8add2ed7c026a25aec2e2fa3c31a8006b164c0a854f790ac3d6ec18d434c6336fae3ebef0dc26a0870ee89d4ebba3aba613255e63e9ccdfab2901b04134585cf54a4c6a0be4d04821ab0df24dba77b0e51b5f2abb8abdc502d63192c95a73f0fb54c93aca894ab78bc31d3168872d449a261a03833238ab392e7301044a573c9e9bfda421032cb4dabf848d39fb
p_lower_bits = 0x437f6c8d0d9303f440a9
q = 0xc69dd70811f543df27a8070b57275cdf82ee76ed685aff76eeaaa76715f8a424bcfd8c1d1db67f92e16376abe6adecf9946f4005c36ddb26176aef796a0e847294ec074f070deac6d3d5e68a5039ee6beb6caaa9eb7de733a45d693dbd9a40e46cf34e44b19c0d7bf1c31a1f1f3b4e1ac7444184e66d048a2d2ede55e4dffae63851b2c98969c43a2c70fc8bd97d49097d5af0b341aa08efd8ee99d7625f5e02ee5760c02ebae7171841f96616ca985ad49db817de958202a5683f553630ef793519a2fa246d36be51bceb05f4cb85f50aa8f0b0ea971b2ddbc053efda5d5a6e61539b773fbcdef5f4158b7de8e988aa0c60740818103513e749c1e2d629c733
dp = 0x3c747767abaf1a7e9b4a96766227ae9a3aaa7f0075379f1a5a74a33089f6399141ccd4f33ce3ecdd9c72d3b948289ba8ed919d28388a0ed78740f3c28c341adbc4b03ac03e2cb70c711c902fe0daedd36f3bf9fd568404d04e0630a1cb2739c0befe42d34fed191892459d438c8a5bc3d71fd899cf99780053a1de55a648ee85e576808cd6e1e239813378b5b2d54dd27dc92a836555940a9cc13972e65224ff86967e8f50c1b3650e2b666015e1f24e56028fa8b4414255fae4830d06bfeadada8cbbc929d4e95f7052344be26ceea5fec2cdb6dd6368e5d5e7291946da65eabbd1ce1ce0eea12b90d757b681b3f5bd8a10c9e5f70f59891c0275a1bef869b9
dq_upper_bits = 0x668677c79cad84b99ed8e7b9fce53ed5c9da9add762ef30c4bab1ffae0a696e4b80211dfbdc4c519e6
e = 65537
p = 0xd9a88ceb5b19d65e1c57467c8726fb1e619564a37a825fcd0e2d0e09b857b1afbe7e3076d5d6ee499239bf64ae0589dbee172fe260b49170aa3b9675a7dbc2497d7623fb3b3c406d793347b772473a4c7e2ba47e12c7aa7106e9858173db38ea410b58c7112639a7fb22f83d3af076c8ba7aa8b3cac5ecfbad649fecb6a3670712e49e4a71de841ae1adb2cea4f3c282d07233657783226a95d4db0e7f10bd7d0fd99826ce53d972bd297b343ffd6a39f983e5e339816f8e53b6abe83acc978841063c2273529cd07255098ce9dc7d8b7d1b6aaaf90ad8d9b01ac3598ad8732b36baa6bf72d9c331117006452f4d70c4e34cff6f1a1b437f6c8d0d9303f440a9

N = p*q

phi = (p-1)*(q-1)
d = pow(e,-1,phi)
assert isPrime(p) and isPrime(q) and p*q == N
assert d % (p-1) == dp
assert hex(N).startswith(hex(N_upper_bits))
assert hex(p).endswith(hex(p_lower_bits)[2:])
assert hex(d % (q-1)).startswith(hex(dq_upper_bits))
from Crypto.PublicKey import RSA

key = RSA.construct((N,e,d,p,q))
pem = key.export_key('PEM')
print(pem.decode())
```

 ```bash
 python3 solver.py > private
 chmod 600 private
 ```

We can now login to target SSH service using this private key as `root` user.

```bash
ssh -i private root@18.218.124.8 -p2222
Welcome to Alpine!

The Alpine Wiki contains a large amount of how-to guides and general
information about administrating Alpine systems.
See <http://wiki.alpinelinux.org/>.

You can setup the system with the command: setup-alpine

You may change this message by editing /etc/motd.

9a20110e7812:~# cat flag.txt
ACVCTF{1nst34d_u_c4n_g1v3_fu11_k3y_:D}
```
