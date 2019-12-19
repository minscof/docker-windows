Windows 10 Home 

Run in a command prompt as administrator:

Install Hyper-V:

cd \users\user\docker
dir /b %SystemRoot%\servicing\Packages\*Hyper-V*.mum >hyper-v.txt
for /f %i in ('findstr /i . hyper-v.txt 2^>nul') do dism /online /norestart /add-package:"%SystemRoot%\servicing\Packages\%i"
del hyper-v.txt
Dism /online /enable-feature /featurename:Microsoft-Hyper-V -All /LimitAccess /ALL
pause

Install Containers:

cd \users\user\docker
dir /b %SystemRoot%\servicing\Packages\*containers*.mum >containers.txt
for /f %i in ('findstr /i . containers.txt 2^>nul') do dism /online /norestart /add-package:"%SystemRoot%\servicing\Packages\%i"
del containers.txt
Dism /online /enable-feature /featurename:Containers -All /LimitAccess /ALL
pause


Edit registry keys:
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion" /f /v EditionID /t REG_SZ /d "Professional"
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion" /f /v ProductName /t REG_SZ /d "Windows 10 Pro"

Download and run official Docker Installer For Windows


REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion" /v EditionID /t REG_SZ /d "Core"
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion" /v ProductName /t REG_SZ /d "Windows 10 Home"