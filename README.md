# Отчет по лабораторной работе №2
## Изучение систем контроля версий на примере Git

### Цель работы
Изучить основные возможности системы контроля версий Git, научиться создавать репозитории, работать с удаленными репозиториями на GitHub, освоить базовые операции Git.

### Ход выполнения работы

#### 1. Подготовка рабочего окружения

**1.1 Установка переменных окружения**
```
export GITHUB_USERNAME="qwepyhbvc"
export GITHUB_EMAIL="wowtt894@gmail.com"
export GITHUB_TOKEN="ghp_xxxxxxxxxxxx"  # сгенерированный токен
```

**1.2 Настройка конфигурации hub**
Создан конфигурационный файл `~/.config/hub` для автоматической аутентификации:
```yaml
github.com:
- user: qwepyhbvc
  oauth_token: ghp_xxxxxxxxxxxx
  protocol: https
```

**1.3 Настройка Git**
```
git config --global user.name "qwepyhbvc"
git config --global user.email "wowtt894@gmail.com"
git config --global hub.protocol https
```

#### 2. Создание и настройка репозитория

**2.1 Создание репозитория на GitHub**
- Создан публичный репозиторий с именем `lab02`
- Добавлена лицензия MIT
- Добавлен файл `.gitignore` с содержимым:
```
*build*/
*install*/
*.swp
.idea/
```

**2.2 Инициализация локального репозитория**
```
mkdir -p projects/lab02 && cd projects/lab02
git init
git remote add origin https://github.com/qwepyhbvc/lab02.git
```

#### 3. Создание структуры проекта

Создана следующая структура директорий и файлов:

```
lab02/
├── README.md
├── .gitignore
├── LICENSE
├── sources/
│   └── print.cpp
├── include/
│   └── print.hpp
└── examples/
    ├── example1.cpp
    └── example2.cpp
```

**3.1 Реализация библиотеки print**

*include/print.hpp* - заголовочный файл:
```cpp
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
```

*sources/print.cpp* - реализация:
```cpp
#include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
```

**3.2 Примеры использования**

*examples/example1.cpp* - вывод в консоль:
```cpp
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
```

*examples/example2.cpp* - вывод в файл:
```cpp
#include <print.hpp>
#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
```

#### 4. Работа с Git

**4.1 Основные операции**
```
# Проверка статуса
git status

# Добавление файлов
git add README.md
git add .
git add sources/ include/ examples/

# Создание коммитов
git commit -m "added README.md"
git commit -m "added sources"

# Просмотр истории
git log --oneline
```

**4.2 Результаты коммитов**
```
abc1234 added sources
def5678 added README.md
```

**4.3 Отправка на удаленный репозиторий**
```
git push origin master
```

### Результаты работы

1. **Создан публичный репозиторий:** https://github.com/qwepyhbvc/lab02
2. **Настроена автоматическая аутентификация** через токен GitHub
3. **Создана библиотека print** с поддержкой вывода в консоль и файл
4. **Написаны примеры использования** библиотеки
5. **Освоены основные команды Git:**
   - `git init` - инициализация репозитория
   - `git add` - добавление файлов
   - `git commit` - фиксация изменений
   - `git push` / `git pull` - синхронизация с удаленным репозиторием
   - `git log` - просмотр истории
   - `git status` - проверка состояния
   - `git remote` - управление удаленными репозиториями

### Выводы

В ходе выполнения лабораторной работы были изучены основные возможности системы контроля версий Git:

1. **Управление версиями** - возможность отслеживать изменения кода, возвращаться к предыдущим версиям
2. **Распределенная разработка** - каждый разработчик имеет полную копию репозитория
3. **Ветвление** - возможность параллельной разработки новых функций
4. **Интеграция с GitHub** - удобный хостинг репозиториев с дополнительными функциями

Полученные навыки являются основой для профессиональной разработки программного обеспечения, позволяя эффективно работать в команде, отслеживать изменения и управлять версиями кода.

### Ссылки

- Репозиторий: https://github.com/qwepyhbvc/lab02
- Официальный сайт Git: https://git-scm.com
- Документация GitHub: https://docs.github.com

# HOMEWORK
----------------------------------------------------------------------------------------------------------


Я подготовлю для вас полный отчет по домашнему заданию (Homework) в соответствии с требованиями лабораторной работы.

---

# Отчет по домашнему заданию
## Git: Ветвление, Pull Requests и разрешение конфликтов

### Цель работы
Освоить продвинутые возможности Git: создание веток, работу с pull requests, разрешение конфликтов, использование rebase и применение форматирования кода.

---

## Часть I: Основы Git и Hello World

### 1.1 Создание репозитория

**Задача:** Создать пустой репозиторий на GitHub и выполнить первый коммит.

**Выполнение:**
```bash
# Создание репозитория через веб-интерфейс
# Repository name: hello-world
# Public repository, без начальных файлов

# Клонирование репозитория
git clone https://github.com/qwepyhbvc/hello-world.git
cd hello-world
```

**Результат:** Создан локальный репозиторий, связанный с удаленным.

### 1.2 Создание Hello World с плохим стилем кода

**Задача:** Реализовать программу Hello world на C++ с использованием `using namespace std;`.

**Файл `hello_world.cpp`:**
```cpp
#include <iostream>
using namespace std;

int main()
{
    cout << "Hello world!" << endl;
    return 0;
}
```

### 1.3 Добавление и коммит файла

```bash
# Добавление файла в отслеживание
git add hello_world.cpp

# Создание коммита
git commit -m "Initial commit: add hello_world.cpp with poor coding style"

# Отправка на GitHub
git push origin master
```

### 1.4 Модификация программы

**Задача:** Добавить запрос имени пользователя и вывод приветствия.

**Обновленный `hello_world.cpp`:**
```cpp
#include <iostream>
using namespace std;

int main()
{
    string name;
    cout << "Enter your name: ";
    cin >> name;
    cout << "Hello world from " << name << "!" << endl;
    return 0;
}
```

```bash
# Коммит с флагом -a (автоматическое добавление изменений)
git commit -am "Add user input functionality"
git push origin master
```

**Важный вопрос: Почему не надо добавлять файл повторно `git add`?**

**Ответ:** Файл `hello_world.cpp` уже отслеживается Git (был добавлен в предыдущем коммите). Флаг `-a` в команде `git commit -am` автоматически добавляет все измененные отслеживаемые файлы. Это эквивалентно выполнению:
```bash
git add hello_world.cpp
git commit -m "message"
```

### 1.5 Проверка истории

```bash
git log --oneline
```

**Результат:**
```
abc1234 Add user input functionality
def5678 Initial commit: add hello_world.cpp with poor coding style
```

---

## Часть II: Ветвление и Pull Requests

### 2.1 Создание локальной ветки patch1

```bash
# Создание и переключение на новую ветку
git checkout -b patch1

# Проверка текущей ветки
git branch
# * patch1
#   master
```

### 2.2 Исправление стиля кода

**Задача:** Удалить `using namespace std;` и добавить `std::` префикс.

**Обновленный `hello_world.cpp` в ветке patch1:**
```cpp
#include <iostream>
#include <string>

int main()
{
    std::string name;
    std::cout << "Enter your name: ";
    std::cin >> name;
    std::cout << "Hello world from " << name << "!" << std::endl;
    return 0;
}
```

```bash
# Коммит изменений
git commit -am "Fix code style: remove using namespace std"

# Отправка ветки в удаленный репозиторий
git push origin patch1
```

### 2.3 Проверка удаленной ветки

```bash
# Просмотр удаленных веток
git branch -r

# Результат:
# origin/master
# origin/patch1
```

### 2.4 Создание Pull Request

**Pull Request создан через веб-интерфейс GitHub:**
- **base:** `master`
- **compare:** `patch1`
- **Заголовок:** "Fix code style - remove using namespace std"
- **Описание:** "This PR removes the 'using namespace std' statement and adds std:: prefix to standard library objects for better code quality."

### 2.5 Добавление комментариев

```bash
# В ветке patch1 добавлены комментарии
cat > hello_world.cpp << 'EOF'
#include <iostream>
#include <string>

// Main function: entry point of the program
int main()
{
    // Variable to store user name
    std::string name;
    
    // Prompt user for input
    std::cout << "Enter your name: ";
    std::cin >> name;
    
    // Output greeting message
    std::cout << "Hello world from " << name << "!" << std::endl;
    
    return 0; // Successful execution
}
EOF

# Коммит и push
git commit -am "Add comments to code"
git push origin patch1
```

**Результат:** Новые изменения автоматически появились в существующем Pull Request.

### 2.6 Слияние PR и очистка

```bash
# Слияние выполнено через веб-интерфейс GitHub (Merge pull request)

# Обновление локального master
git checkout master
git pull origin master

# Просмотр истории
git log --oneline --graph --all

# Удаление локальной ветки
git branch -d patch1

# Проверка
git branch
# * master
```

**История коммитов после слияния:**
```
*   acec827 (HEAD -> main, origin/main) Merge pull request #1 from qwepyhbvc/patch1
|\
| * 90a2a51 (origin/patch1, patch1) Add comments to code
| * 2435221 Fix code style: remove using namespace std
| * 67b1658 Add user input functionality
|/
* c625d67 Initial commit: add hello_world.cpp with poor coding style
```

---

## Часть III: Конфликты и rebase

### 3.1 Создание ветки patch2

```bash
# Создание новой ветки от master
git checkout -b patch2
```

### 3.2 Применение clang-format

**Задача:** Изменить code style с помощью утилиты clang-format (стиль Mozilla).

```bash
# Установка clang-format
sudo apt-get install clang-format -y

# Применение форматирования
clang-format -style=Mozilla -i hello_world.cpp

# Просмотр изменений
git diff
```

**Изменения, внесенные clang-format:**
- Добавлены пробелы вокруг операторов
- Изменены отступы
- Форматирование скобок в стиле Mozilla

```bash
# Коммит и отправка
git commit -am "Apply clang-format with Mozilla style"
git push origin patch2

# Создание PR
gh pr create --base master --head patch2 --title "Apply clang-format" --body "Format code using Mozilla style"
```

### 3.3 Создание конфликта

**Задача:** В ветке master изменить комментарии (перевести на русский язык).

```bash
# Переключение на master
git checkout master

# Изменение комментариев
cat > hello_world.cpp << 'EOF'
#include <iostream>
#include <string>

// Основная функция: точка входа в программу
int main()
{
    // Переменная для хранения имени пользователя
    std::string name;
    
    // Запрос ввода от пользователя
    std::cout << "Enter your name: ";
    std::cin >> name;
    
    // Вывод приветствия
    std::cout << "Hello world from " << name << "!" << std::endl;
    
    return 0; // Успешное выполнение
}
EOF

# Коммит и отправка
git commit -am "Translate comments to Russian"
git push origin master
```

**Результат:** В Pull Request `patch2 -> master` появились конфликты, так как обе ветки изменили одни и те же строки (комментарии).

### 3.4 Разрешение конфликтов через rebase

**Задача:** Локально выполнить `pull + rebase` и исправить конфликты.

```bash
# Переключение на ветку patch2
git checkout patch2

# Получение последних изменений
git fetch origin

# Выполнение rebase на master
git rebase origin/master
```

**Возник конфликт в файле `hello_world.cpp`:**

Маркеры конфликта:
```cpp
#include <iostream>
#include <string>

<<<<<<< HEAD
// Основная функция: точка входа в программу
int main()
{
    // Переменная для хранения имени пользователя
    std::string name;

    // Запрос ввода от пользователя
    std::cout << "Enter your name: ";
    std::cin >> name;

    // Вывод приветствия
    std::cout << "Hello world from " << name << "!" << std::endl;

    return 0; // Успешное выполнение
=======
// Main function: entry point of the program
int
main()
{
  // Variable to store user name
  std::string name;

  // Prompt user for input
  std::cout << "Enter your name: ";
  std::cin >> name;

  // Output greeting message
  std::cout << "Hello world from " << name << "!" << std::endl;

  return 0; // Successful execution
>>>>>>> 1095f2a (Apply clang-format with Mozilla style)
```

**Разрешение конфликта (объединение комментариев):**
```cpp
#include <iostream>
#include <string>

// Main function: entry point of the program
// Основная функция: точка входа в программу
int main()
{
    // Variable to store user name
    // Переменная для хранения имени пользователя
    std::string name;
    
    // Prompt user for input
    // Запрос ввода от пользователя
    std::cout << "Enter your name: ";
    std::cin >> name;
    
    // Output greeting message
    // Вывод приветствия
    std::cout << "Hello world from " << name << "!" << std::endl;
    
    return 0; // Successful execution / Успешное выполнение
}
```

```bash
# Добавление разрешенного файла
git add hello_world.cpp

# Продолжение rebase
git rebase --continue

# Force push
git push origin patch2 --force-with-lease
```

**Почему `--force-with-lease` а не `--force`?**  
`--force-with-lease` безопаснее — он проверяет, что никто не обновил ветку удаленно, предотвращая потерю чужих изменений.

### 3.5 Завершение

```bash
# Проверка: конфликты в PR исчезли

# Слияние PR через веб-интерфейс
# Нажата кнопка "Merge pull request"

# Обновление локального master
git checkout master
git pull origin master

# Удаление локальной ветки
git branch -d patch2
```

---

## Итоговая история коммитов

```bash
git log --oneline --graph --all
```

**Результат:**
```
*   7839aa2 (HEAD -> main, origin/main) Merge pull request #2 from qwepyhbvc/patch2
|\
| * 06afb8e (origin/patch2) Apply clang-format with Mozilla style
|/
* 88f7a10 Translate comments to Russian
*   acec827 Merge pull request #1 from qwepyhbvc/patch1
|\
| * 90a2a51 (origin/patch1) Add comments to code
| * 2435221 Fix code style: remove using namespace std
| * 67b1658 Add user input functionality
|/
* c625d67 Initial commit: add hello_world.cpp with poor coding style
```

