:ollama_pull
REM Скрипт для загрузки большой модели при ошибках и обрыве связи

@echo off
chcp 65001 > NUL

set /p model="Введите названия модели: "

:loop
ollama pull %model%
if !errorlevel! neq 0 (
    echo 'Ошибка при загрузке модели, повторяем попытку...'
    timeout /t 5 >nul
) else (
    echo 'Загрузка завершена!'
    chcp 866 > NUL
    goto :eof
)
goto loop
:eof
