# multiclipboard
#The multiclipboard is a simple command-line utility that allows users to save, load, list, and delete data (text) from the clipboard using JSON files as a #storage mechanism. The script serves as a basic clipboard manager with the ability to store multiple items in a structured way.
import sys
import clipboard
import json

def savedata(filepath,data):
    with open(filepath,'w') as f:
        json.dump(data,f)
def loaddata(filepath):
    try:
        with open(filepath,'r') as f:
            data=json.load(f)
            return data
    except:
        return {}

#savefile('my1st.json',{'clip':'board'})
saveddata='my1st.json'
if len(sys.argv)==2:
    command=sys.argv[1]
    data=loaddata(saveddata)
    if command=='save':
        key=input('enter key')
        data[key]=clipboard.paste()
        savedata(saveddata,data)
        print("data saved")

    elif command=='list':
        print(data)
    elif command=='load':
        key=input('enter key')
        if key in data:
            print(data[key])
        else:
            print("not found")
    elif command=='del':
        key=input('enter key')
        if key in data:
            del data[key]
            savedata(saveddata,data)
        else:
            print("not found to del")
    else:
        print('Unknown Command')
    
else:
    print('please include exactly one command')
