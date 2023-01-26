1. ssh into machine
2. execute `sudo -l` to see you can execute the `/home/pupil/random_message.py` file with `/usr/bin/python3` with `root` privileges
3. note that we cannot modify the script in question
4. but we see, that it imports the `random` python package
5. in the same directory, we create a file `random.py` and fill it with:
```
import os
os.system("/bin/bash")
```
Now, the `random_message.py` will import this script (and execute while doing so) when being run. 
6. Run `random_message.py` again and gain a shell as `root`
