# Phantom.PM

Конвертер текстовой информации о звонке на мини-АТС генерируемой программно-аппаратным комплексом MDIS Phantom

Пакет для разбора NWU и NTF-файлов на составляющие.

## About

Phantom - технический и программный комплекс по перехвату телефонных разговоров на мини-АТС ipLDK-300 Office. Перехваченные звонки записываются в директорию `<records>` с расширением "nwu", запись разговора ведется "наживую", т.е. от начала и до конца разговора в nwu-файлы производится запись. По окончанию разговора в директорию `<notification>` добавляется мета-файл с расширением "ntf". Имена "ntf" и "nwu"-файлов одинаковые, 16-ое представление внутерннего ID записи.

MDISConverter - служба, позволяющая произвести конвертацию аудиозаписи в mp3-формат ожидает появление мета-файла в директории `<notification>`, после чего производится поиск "nwu"-файла

### Scheme 
       
#### Structure NTF
NTF - мета-файл, содержит только текстовую информацию о звонка:
```
0000 - 0001 [001] - канал звонка
0001 - 0007 [007] - ?!
0008 - 0009 [001] - тип звонка
0010 - 0012 [002] - ?!
0012 - 0020 [008] - дата и время начала звонка в tick'ах
0020 - 0028 [008] - дата и время конца звонка в tick'ах
0028 - 0060 [032] - номер телефона на который позвонили
0060 - 0092 [032] - строка импульсного набора
0092 - 0132 [040] - номер телефона с которого звонили
0133 - 0138 [007] - ?!
0139 - 0147 [008] - id звонка в системе Phantom
0148 - 0463 [315] - ?!
0464 - 0592 [128] - полная строка импульсного набора
0592 - 1104 [512] - маска для разбора полной строки импульсного набора
1360 - 1616 [256] - строка переадресаций звонка
1616 - 1872 [256] - строка как-то связанная со строкой переадресации звонка
1872 - 1880 [008] - время дозвона
```

#### Structure NWU
NWU - файл, который содержит и текстовую информацию о звонке и запись разговора. В частности, весь файл NTF хранится в NWU с 40 по 1884 байт

## TODO
* извлечение аудио-записи и дешифровка
