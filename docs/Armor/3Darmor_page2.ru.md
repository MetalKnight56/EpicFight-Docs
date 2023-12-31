# Другие решения проблем со сломанной 3D Броней
Пожалуйста, имейте в виду, что эти решения могут быть не так эффективны, как ручное исправление брони в программе Blender. Эти инструменты в основном предназначены для разработчиков мод-паков и модов, чтобы проверять свою броню. Если вы хотите правильно исправить броню и убедиться, что она работает в игре, перейдите по ссылке _**[Custom 3D armor Resource Pack](armor/page1)**_


***
## **💡 Создание визуально безупречной брони с использованием режима отладки брони**

В Minecraft вы можете включить режим отладки брони, нажав комбинацию клавиш F3+Y. Это создаст модель брони для каждого кадра, чтобы проверить результат алгоритма создания модели. Однако это может значительно снизить частоту кадров в секунду (Fps), поэтому я не рекомендую включать эту функцию в обычных ситуациях.

![image](https://user-images.githubusercontent.com/79469058/168334604-6542eff4-c77e-4ef2-a71a-79ddeef91a9a.png)

_Это сообщение будет отображаться при переключении режима отладки брони._
***
### **📦 Экспорт моделей в виде Ресурспака**

На экране настроек мода, вы можете увидеть кнопку "Экспорт моделей брони".  Оно экспортирует все созданные модели брони из кэша в виде ресурспака. Затем примените ресурспак и вам не придется отлаживать модели брони каждый раз при запуске Minecraft.

![image](https://user-images.githubusercontent.com/79469058/168339170-1965ad10-eb2a-4ab4-919e-3f5d5b0480fd.png)
***
## **💡Если предыдущее решение не работает для экспорта моделей брони в виде ресурспака, вы можете попробовать следующую альтернативу:**


Есть пользовательские доспехи, которые не могут быть исправлены, даже при использовании режима отладки. Это происходит потому, что существуют различные способы отображения пользовательских доспехов. Вы можете выбрать альтернативный способ, чтобы хотя бы сделать их видимыми.

Сначала вам необходимо заставить их использовать модель по умолчанию. Вы можете создать собственную модель брони в следующей папке,

### assets/`modid`/animmodels/armor/`item_name.json`

В файле item_name.json введите следующий код, чтобы назначить модель по умолчанию для брони.

```
{
    "parent": "epicfight:armor/model_name"
}
```
Доступные имена_моделей: `helmet_default, chestplate_default, leggings_default, boots_default`

Затем вы можете изменить текстуру пользовательской брони, чтобы она соответствовала формату текстуры модели по умолчанию.

![sample](https://user-images.githubusercontent.com/79469058/168444508-f1fb4ebe-5949-40ca-9015-7e920f1e6508.png)

_Отображение текстур стандартной модели брони_

Сохраните свои текстуры, но избегайте перезаписи существующей текстуры, поскольку это может сломать стандартную модель. Вместо этого сохраните свою текстуру по следующему пути: assets/modid/`существующий_путь`/epicfight/`имя_текстуры`. Например: "assets/minecraft/textures/models/armor/iron_layer_1.png". Вы будете использовать: "assets/minecraft/textures/models/armor/epicfight/iron_layer_1.png"

## **💡 Добавление прозрачности пользовательским доспехам**
***

Некоторые пользовательские доспехи имеют прозрачность в своей текстуре. Вы можете сделать их прозрачными в боевом режиме, добавив следующие строки.

```
{
    "render_properties": {
        "transparent": true
    },
        "vertices": {
                ...
        }
}
```