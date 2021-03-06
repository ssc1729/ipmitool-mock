# ipmitool-mock

[![Build Status](https://dev.azure.com/ssc1729/ipmitool-mock/_apis/build/status/ssc1729.ipmitool-mock.build?branchName=main)](https://dev.azure.com/ssc1729/ipmitool-mock/_build/latest?definitionId=7&branchName=main)

`ipmitool-mock` is utility to mock the functionality of [ipmitool](https://github.com/ipmitool/ipmitool). 

# How to Install?

## From the Binary Releases (For Linux)

```
# download release file
>> wget https://github.com/ssc1729/ipmitool-mock/releases/download/<version>/ipmitool-linux.zip

# unzip release file
>> unzip ipmitool-linux.zip

# copy binary file to /use/local/bin, need sudo privileges
>> sudo cp ipmitool /usr/local/bin/

# run ipmitool-mock commands
>> ipmitool sdr
>> ipmitool sdr elist
```

## From Source code

```
# clone repository, alternativly download from latest release
>> git clone https://github.com/ssc1729/ipmitool-mock

# create python virtual environment
>> cd ipmitool-mock
>> python3 -m virtualenv venv

# activate virtualenv
# this command changes on different operating systems, check below link for more info
# https://docs.python.org/3/tutorial/venv.html#creating-virtual-environments
>> source venv/bin/activate

# install requirements
>> pip3 install -r requirements.txt

# generate binary file
>> cd src
>> pyinstaller --onefile --name ipmitool ipmitool-mock.py

# copy binary file to /use/local/bin, need sudo privileges
# for windows, add ipmitool binary file to environment path
>> cd dist
>> sudo cp ipmitool /usr/local/bin/

# run ipmitool-mock commands
>> ipmitool sdr
>> ipmitool sdr elist
```

*Note: For Windows use PowerShell*

## Sample output

```
>> ipmitool -U <username> -P <password> sdr
System Fan 1     | 9292 RPM          | ok
System Fan 2     | 9253 RPM          | ok
PS1 Input Power  | 104 Watts         | ok
PS2 Input Power  | 101 Watts         | ok
PS1 Temperature  | 25 degrees C      | ok
PS2 Temperature  | 25 degrees C      | ok
PS1 Status       | 0x00              | ok
PS2 Status       | 0x00              | ok

>> ipmitool -U <username> -P <password> sdr elist
System Fan 1     | 0Ah | ok | 10.1 | 9568 RPM
System Fan 2     | 0Bh | ok | 10.2 | 9807 RPM
PS1 Input Power  | 01h | ok | 11.1 | 115 Watts
PS2 Input Power  | 02h | ok | 11.2 | 107 Watts
PS1 Temperature  | 01h | ok | 11.1 | 23 degrees C
PS2 Temperature  | 02h | ok | 11.2 | 27 degrees C
PS1 Status       | 01h | ok | 11.1 | Presence detected
PS2 Status       | 02h | ok | 11.2 | Presence detected

>> ipmitool -U <username> -P <password> sensor
System Fan 1     | 9650.000   | RPM        | ok    | 300.000   | 500.000   | 700.000   | 25300.000 | 25400.000 | 25500.000
System Fan 2     | 9555.000   | RPM        | ok    | 300.000   | 500.000   | 700.000   | 25300.000 | 25400.000 | 25500.000
PS1 Input Power  | 102.000    | Watts      | ok    | na        | na        | na        | 1700.000  | 1800.000  | 2200.000
PS2 Input Power  | 103.000    | Watts      | ok    | na        | na        | na        | 1700.000  | 1800.000  | 2200.000
PS1 Temperature  | 28.000     | degrees C  | ok    | na        | 5.000     | 16.000    | 53.000    | 60.000    | 65.000
PS2 Temperature  | 25.000     | degrees C  | ok    | na        | 5.000     | 16.000    | 53.000    | 60.000    | 65.000
PS1 Status       | 0x1        | discrete   | 0x0100| na        | na        | na        | na        | na        | na
PS2 Status       | 0x1        | discrete   | 0x0100| na        | na        | na        | na        | na        | na

>> ipmitool -U <username> -P <password> sel
1    | 08/01/2021 | 15:44:56 | Fan #0x96 | Lower Critical going low  | Asserted
2    | 08/01/2021 | 15:44:56 | Fan #0x96 | Lower Non-recoverable going low  | Asserted
3    | 08/01/2021 | 15:44:56 | Fan #0x96 | Lower Non-recoverable going low  | Deasserted
```
