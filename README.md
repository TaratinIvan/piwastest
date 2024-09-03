Windows
=
1. Перейдите по [ссылке](https://github.com/Matsuridayo/nekoray/releases "ссылке")
2. В последнем СТАБИЛЬНОМ релизе во вкладке Assets найти архив под нужную систему, в моём случае `nekoray-3.26-2023-12-09-windows64.zip `
3. Скачайте и разархивируйте архив в удобную для вас директорию
4. ОБЯЗАТЕЛЬНО удалите goodbyedpi встроенным скриптом, если пользовались, и удалите папку
5. Запустите `nekoray.exe` от имени администратора, в качестве ядра выберите x-ray
6. Скопируйте ссылку, выданную Мишей
7. В окне программы нажмите `Ctrl+V`
8. Проставьте чекбокс `Режим системного прокси`
9. Перейдите в `Настройки` -> `Настройки маршрутов` -> `Базовые маршруты`
10. Вставьте список адресов, как показано ниже. (Вы можете добавлять нужные вам по аналогии) Выставьте `Otbound по-умолчанию` `bypass` Нажмите `OK` 
```
x.com
instagram.com
regexp:.*rutracker.*
twitter.com
regexp:.*twimg.*
chatgpt.com
regexp:.*openai.*
claude.ai
spotify.com
regexp:.*youtube.*
regexp:.*youtu\.be.*
regexp:.*googlevideo.*
regexp:.*ytimg.*
```
![](https://files.catbox.moe/8v16u4.png)
11. `ПКМ` -> `Запустить` Наслаждайтесь!!! :tada::tada::tada:<br>
12. (Необязательно) Нажмите `Программа`, выставите галочки напротив `Запускаться вместе с системой` и `Запомнить последний профиль`. Теперь программа запускается в фоновом режиме при запуске Windows.

Android
=
1. Скачайте приложение [v2rayNG](https://play.google.com/store/apps/details?id=com.v2ray.ang&hl=ru)
2. Нажмите на иконку `+` -> `Добавить из буфера обмена`
3. Перейдите в `Настройки` -> `Пользовательские правила`
4. Выставьте в разделе `Проксируемые сайты`, которые заблокированы, через запятую по аналогии: `regexp:.*openai.*,regexp:.*chatgpt.*,regexp:.*oai.*`
5. В разделе `Прямые` выставьте сайты, которые не должны проксироваться: `regexp:.*\.ru,regexp:.:*vk.com,geoip.ru`
6. В `Настройки` в пункте `Прокси для выбранных приложений` выберите приложения, в которых вам НУЖЕН обход. В основном это браузер, твиттер, инста и ютуб.
7. Не забудьте запустить службу и добавить иконку приложения в шторку сверху.

# Known Issues

## Microsoft Store (Windows)

Для корректной работы Microsoft Store требуется добавить соответствующий AppContainer в исключения из [замыкания на себя](https://ab57.ru/cmdlist/checknetisolation.html).

Добавление Microsoft Store в исключения:

```powershell
Get-ChildItem -Path "HKCU:\Software\Classes\Local Settings\Software\Microsoft\Windows\CurrentVersion\AppContainer\Mappings" | 
Get-ItemProperty -Name DisplayName | 
Where-Object { $_.DisplayName -like "Microsoft Store" } | 
ForEach-Object { CheckNetIsolation LoopbackExempt -a -p="$($_.PSChildName)" }
```

Rollback (удаление из исключений):

```powershell
Get-ChildItem -Path "HKCU:\Software\Classes\Local Settings\Software\Microsoft\Windows\CurrentVersion\AppContainer\Mappings" | 
Get-ItemProperty -Name DisplayName | 
Where-Object { $_.DisplayName -like "Microsoft Store" } | 
ForEach-Object { CheckNetIsolation LoopbackExempt -d -p="$($_.PSChildName)" }
```
