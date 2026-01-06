Шляхи (приклад)

Папка світів (Prospects):

C:\Users\user\AppData\Local\Icarus\Saved\PlayerData\76561199354886998\Prospects


Гра:

D:\GAMES_D\steamapps\common\Icarus\Icarus.exe

1. Ініціалізація Git (один раз)

Відкрий PowerShell:

cd "C:\Users\user\AppData\Local\Icarus\Saved\PlayerData\76561199354886998\Prospects"
git init
git remote add origin https://github.com/USERNAME/icarus-prospects.git
git add .
git commit -m "Initial Icarus prospects"
git push -u origin main


Репозиторій на GitHub має бути порожній

2. .gitignore

Створи файл Prospects/.gitignore

*.log
*.tmp
*.bak
*.cache
*.old

**/Temp/
**/Logs/


Це захищає репозиторій від сміття та логів.

3. PowerShell-скрипт запуску

Створи файл icarus.ps1 (можна зберігати де зручно):

$prospectsPath = "C:\Users\user\AppData\Local\Icarus\Saved\PlayerData\76561199354886998\Prospects"
$icarusExe = "D:\GAMES_D\steamapps\common\Icarus\Icarus.exe"

Set-Location $prospectsPath
git pull

$proc = Start-Process -FilePath $icarusExe -PassThru
Wait-Process -Id $proc.Id

git add .
if (-not (git diff --cached --quiet)) {
    git commit -m "Auto save: $(Get-Date -Format 'yyyy-MM-dd HH:mm')"
    git push
}

4. Дозвіл на запуск скриптів (один раз)
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned

5. Як грати

❗ ВАЖЛИВО:
НЕ запускай Icarus напряму через Steam

Правильний запуск:

.\icarus.ps1

Рекомендації

Для solo — працює ідеально

Для коопу:

push робить тільки хост

всі інші — тільки pull

Один світ = один репозиторій

Steam Cloud має бути вимкнений
