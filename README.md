# Развёртывание Flutter приложения на GitHub Pages

#### __Создание репозитория__
* Создаём стандартный, публичный репозиторий в GitHub

#### **Подготовка проекта**
* Находясь в корне проекта открываем терминал и вызываем команду flutter build web
* Переходим в директорию /build/web/
* В файле index.html находим строчку <base href="/"> и меняем href="/" на название репозитория GitHub (Пример href="/flutter_page/")
* Добавляем файлы дирректории /build/web/ в репозиторий GitHub

#### __Развёртывание__
* Переходим в Settings репозитория GitHub
* Открываем вкладку Pages
* Выбираем ветку на которую был запушен проект или ветку с которой будет выполняться развёртывание (обычно main)
* Ждём некоторое время, переодически обновляя страницу
* После появления кнопки "Visit Page" переходим по ней

# Парсинг текста/markdown с GitHub/Docsify в Flutter приложении
#### __Парсинг с GitHub репозитория__
* В репозитори создать файл для парсинга в формате .txt или .md
* __Важно!__ Для удачного парсинга ссылка на файл должна иметь вид:
```
https://raw.githubusercontent.com/Имя пользователя GitHub/Название репозитория/Название ветки/Название файла
```
* Пример:
```
https://raw.githubusercontent.com/Y0ungM0rris/flutter_page/main/README.md
```
#### __Парсинг с Docsify__
* Создать и развурнуть страницу docsify по [инструкции](https://y0ungm0rris.github.io/docsify_page/#/) (https://y0ungm0rris.github.io/docsify_page/#/)
* __Важно!__ Для удачного парсинга ссылка на страницу docsify должна иметь вид:
```
https://ссылка на развёрнутую docsify страницу/README.md
```
* Пример:
```
https://y0ungm0rris.github.io/docsify_page/README.md
```
#### __Код парсера можно взять ниже или по ссылке в примере:__
```dart
var link = Uri.tryParse('ссылка на документ');

FutureBuilder<http.Response>
                  (
                    future: http.get(link!),
                    builder: (context, snapshot) {
                      if (snapshot.hasData) {
                        String markdown = snapshot.data!.body;
                        return MarkdownBody(data: markdown);
                      } else if (snapshot.hasError) {
                        return Text('Ошибка: ${snapshot.error}');
                      }
                      return const CircularProgressIndicator();
                    }
                )
```
