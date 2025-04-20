## 🚡 Quick Fix: npm Script Execution Error

### ⚠️ Problem
When trying to run `npm install`, you encounter this error:
```powershell
npm : File C:\Program Files\nodejs\npm.ps1 cannot be loaded because running scripts is disabled on this system.
At line:1 char:1
+ npm i
+ ~~~
    + CategoryInfo          : SecurityError: (:) [], PSSecurityException
    + FullyQualifiedErrorId : UnauthorizedAccess


Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
