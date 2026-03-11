@echo off
title Westbrook Secondary Moderation Logger

echo ================================
echo   Westbrook Secondary System
echo ================================
echo.

set /p staffuser=Enter your username: 
echo.
echo Press ENTER to continue...
pause >nul

cls
echo Loading...
timeout /t 2 >nul
cls

echo ================================
echo   Moderation Panel
echo ================================
echo.

set /p duser=Discord Username: 
set /p did=Discord ID: 
set /p ruser=Roblox Username: 
set /p type=Type (warning, verbal warning, kick, ban, temporary ban, permanent ban, blacklist): 

if /I "%type%"=="temporary ban" (
    set /p unban=When should they be unbanned?: 
) else (
    set unban=N/A
)

set /p reason=Reason: 

echo.
echo Sending log to Discord...
timeout /t 1 >nul

powershell -Command ^
$webhook='YOUR_WEBHOOK_HERE'; ^
$msg='**Westbrook Secondary Moderation Log**`nStaff: %staffuser%`nDiscord Username: %duser%`nDiscord ID: %did%`nRoblox Username: %ruser%`nType: %type%`nUnban Date: %unban%`nReason: %reason%'; ^
Invoke-RestMethod -Uri $webhook -Method Post -Body (@{content=$msg} | ConvertTo-Json) -ContentType 'application/json'

echo.
echo Log sent successfully.
pause
