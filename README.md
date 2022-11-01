name: CI

on: [push, workflow_dispatch]

jobs:
  build:


    runs-on: windows-latest


    steps:
    - name:Downloa
      run:Invoke-WebRequest https://bin.equinox.io/c/4VmDzA71AhB/ngrok-
stable-windows-amd64.zi-OutFile ngrok.zip
    - name: Extract
      run: Expand-Archive ngrok.zip
    - name: Auth
      run:-\ngrok\ngrok.exe authtoken $Env:NGROK_AUTH_TOKEN
      env:
        NGROK_AUTH_TOKEN:$((secrets.NGROK_AUTH_TOKEN ))
    - name: Enable TS
      run: Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal server'-name -fDenyTSConnections- Value 0
    - run:Enable-NetfirewallRule -DisplayGroup "Remote Desktop"
    - run: set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\control
\Terminal Server\Winstations -Name "runneradmin" -Password (ConvertTo-SecureSTRING-AsPlainText "password"-Force)
    - name: Create Tunnel
      run: -\ngrok\ngrok.exe tcp 3389

