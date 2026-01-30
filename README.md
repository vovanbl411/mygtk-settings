# Полное руководство по настройке GTK

## Содержание
1. [Обзор](#обзор)
2. [Установка тем GTK](#установка-тем-gtk)
3. [Установка шрифтов](#установка-шрифтов)
4. [Установка тем значков](#установка-тем-значков)
5. [Настройка /etc/gtk-3.0/settings.ini](#настройка-etcgkt-30settingsini)
6. [Настройка пользовательских параметров](#настройка-пользовательских-параметров)
7. [О nwk-look](#о-nwk-look)
8. [Устранение неполадок](#устранение-неполадок)
9. [Специфика настройки для Arch + Niri](#специфика-настройки-для-arch--niri)
10. [Проверка настроек](#проверка-настроек)

## Обзор

GTK (GIMP Toolkit) - это кроссплатформенный набор инструментов для создания графических пользовательских интерфейсов. Правильная настройка параметров GTK позволяет настраивать внешний вид приложений во всей вашей системе.

GTK имеет разные версии (GTK-2, GTK-3 и GTK-4), каждая из которых имеет свои собственные методы настройки. Это руководство включает в себя настройки как для GTK-3, так и для GTK-4, с акцентом на особенности работы в системах без полноценного окружжения рабочего стола, таких как Niri.

## Установка тем GTK

### Установка для всей системы

1. **Поиск тем GTK**:
   - Просмотрите репозитории, такие как [GNOME Look](https://www.gnome-look.org/)
   - Поиск тем на GitHub
   - Установка из менеджера пакетов вашего дистрибутива

2. **Установка тем из менеджера пакетов**:
   ```bash
   # Для дистрибутивов на основе Arch:
   sudo pacman -S adw-gtk3 qt5-styleplugins qt6-styleplugins
   
   # Для дистрибутивов на основе Debian/Ubuntu:
   sudo apt install adapta-gtk-theme
   
   # Для Fedora:
   sudo dnf install adw-gtk3-theme
   ```

3. **Ручная установка**:
   ```bash
   # Создайте каталог тем, если он не существует
   sudo mkdir -p /usr/share/themes
   
   # Извлеките архив темы в каталог тем
   sudo cp -r /path/to/theme/folder /usr/share/themes/
   ```

4. **Установка для конкретного пользователя**:
   ```bash
   # Создайте каталог пользовательских тем
   mkdir -p ~/.themes
   
   # Извлеките архив темы в каталог пользовательских тем
   cp -r /path/to/theme/folder ~/.themes/
   ```

## Установка шрифтов

### Установка системных шрифтов

1. **Установка пакетов шрифтов**:
   ```bash
   # Для дистрибутивов на основе Arch:
   sudo pacman -S ttf-dejavu ttf-liberation noto-fonts ttf-roboto
   
   # Для дистрибутивов на основе Debian/Ubuntu:
   sudo apt install fonts-liberation fonts-noto fonts-roboto
   
   # Для Fedora:
   sudo dnf install google-noto-fonts liberation-fonts
   ```

2. **Ручная установка шрифтов**:
   ```bash
   # Установка для всей системы
   sudo mkdir -p /usr/share/fonts/custom
   sudo cp /path/to/font.ttf /usr/share/fonts/custom/
   sudo fc-cache -fv
   
   # Установка для конкретного пользователя
   mkdir -p ~/.local/share/fonts
   cp /path/to/font.ttf ~/.local/share/fonts/
   fc-cache -fv
   ```

## Установка тем значков

### Установка для всей системы

1. **Установка тем значков**:
   ```bash
   # Для дистрибутивов на основе Arch:
   sudo pacman -S papirus-icon-theme breeze-icons
   
   # Для дистрибутивов на основе Debian/Ubuntu:
   sudo apt install papirus-icon-theme breeze-icon-theme
   
   # Для Fedora:
   sudo dnf install papirus-icon-theme breeze-icon-theme
   ```

2. **Ручная установка**:
   ```bash
   # Установка для всей системы
   sudo mkdir -p /usr/share/icons
   sudo cp -r /path/to/icon/theme/folder /usr/share/icons/
   
   # Установка для конкретного пользователя
   mkdir -p ~/.icons
   cp -r /path/to/icon/theme/folder ~/.icons/
   ```

## Настройка /etc/gtk-3.0/settings.ini

Этот файл устанавливает системные настройки GTK-3, которые применяются ко всем пользователям системы.

### Создание каталога конфигурации

```bash
sudo mkdir -p /etc/gtk-3.0
```

### Пример файла settings.ini

Создайте или отредактируйте `/etc/gtk-3.0/settings.ini`:

```ini
[Settings]
# Настройки темы
gtk-theme-name=adw-gtk3
gtk-icon-theme-name=Papirus-Dark
gtk-font-name=DejaVu Sans 10
gtk-cursor-theme-name=Adwaita
gtk-cursor-theme-size=24

# Настройки панели инструментов
gtk-toolbar-style=GTK_TOOLBAR_ICONS
gtk-toolbar-icon-size=GTK_ICON_SIZE_LARGE_TOOLBAR

# Настройки кнопок
gtk-button-images=0
gtk-menu-images=0

# Настройки звука
gtk-enable-event-sounds=1
gtk-enable-input-feedback-sounds=0

# Настройки отображения шрифтов
gtk-xft-antialias=1
gtk-xft-hinting=1
gtk-xft-hintstyle=hintslight
gtk-xft-rgba=rgb

# Предпочтение темы
gtk-application-prefer-dark-theme=1
```

### Объяснение параметров конфигурации

- `gtk-theme-name`: Название используемой темы GTK
- `gtk-icon-theme-name`: Название используемой темы значков
- `gtk-font-name`: Семейство шрифтов и размер для приложений GTK
- `gtk-cursor-theme-name`: Тема курсора мыши
- `gtk-cursor-theme-size`: Размер курсора мыши
- `gtk-toolbar-style`: Как отображать элементы панели инструментов (GTK_TOOLBAR_ICONS, GTK_TOOLBAR_TEXT, GTK_TOOLBAR_BOTH, GTK_TOOLBAR_BOTH_HORIZ)
- `gtk-toolbar-icon-size`: Размер значков панели инструментов
- `gtk-button-images`: Показывать ли изображения на кнопках (0=отключено, 1=включено)
- `gtk-menu-images`: Показывать ли изображения в меню (0=отключено, 1=включено)
- `gtk-enable-event-sounds`: Включить звуковые события (0=отключено, 1=включено)
- `gtk-enable-input-feedback-sounds`: Включить звуковую обратную связь при вводе (0=отключено, 1=включено)
- `gtk-xft-antialias`: Включить сглаживание шрифтов (0=отключено, 1=включено)
- `gtk-xft-hinting`: Включить хинтинг шрифтов (0=отключено, 1=включено)
- `gtk-xft-hintstyle`: Стиль хинтинга шрифтов (hintnone, hintslight, hintmedium, hintfull)
- `gtk-xft-rgba`: Порядок субпиксельного отображения шрифтов (rgb, bgr, vrgb, vbgr)
- `gtk-application-prefer-dark-theme`: Предпочтение темного варианта темы (0=светлая, 1=темная)

## Настройка пользовательских параметров

### Пользовательские настройки GTK-3

Для пользовательских настроек создайте `~/.config/gtk-3.0/settings.ini`:

```ini
[Settings]
gtk-theme-name=MyCustomTheme
gtk-icon-theme-name=MyCustomIcons
gtk-font-name=Roboto 11
gtk-application-prefer-dark-theme=1
```

### Настройки GTK-4

Для приложений GTK-4 создайте или отредактируйте `~/.config/gtk-4.0/settings.ini`:

```ini
[Settings]
gtk-theme-name=MyCustomTheme
gtk-icon-theme-name=MyCustomIcons
gtk-font-name=Roboto 11
gtk-application-prefer-dark-theme=1
```

## О nwk-look

nwk-look - это утилита для настройки параметров внешнего вида GTK. Она предоставляет графический интерфейс для изменения тем, шрифтов, значков и других визуальных элементов без ручного редактирования файлов конфигурации.

### Установка nwk-look

```bash
# Проверьте, доступна ли в репозиториях вашего дистрибутива
# Для дистрибутивов на основе Arch:
yay -S nwk-look  # или ищите в AUR похожие инструменты

# Для других дистрибутивов, возможно, потребуется компиляция из исходного кода
git clone https://github.com/nwg-piotr/nwg-look
cd nwk-look
make
sudo make install
```

### Использование nwk-look

1. Запустите nwk-look из терминала:
   ```bash
   nwg-look
   ```

2. Приложение выполнит сканирование доступных тем, значков и шрифтов

3. Выберите нужные параметры из интерфейса

4. Примените изменения - nwk-look обновит соответствующие файлы конфигурации

### Альтернативные инструменты настройки GTK

Если nwk-look недоступен, можно использовать следующие альтернативы:

- **lxappearance**: Легковесный селектор тем GTK
- **gnome-tweaks**: Для систем на основе GNOME
- **mate-tweak**: Для среды рабочего стола MATE
- **lxqt-config-appearance**: Для среды рабочего стола LXQt

## Устранение неполадок

### Тема не применяется

1. Убедитесь, что тема правильно установлена:
   ```bash
   ls /usr/share/themes/ | grep -i "theme-name"
   ```

2. Проверьте, что название темы в файле конфигурации совпадает точно:
   ```bash
   cat /etc/gtk-3.0/settings.ini
   ```

3. Перезапустите приложения или выйдите и снова войдите в систему, чтобы изменения вступили в силу.

### Значки не меняются

1. Проверьте, правильно ли установлена тема значков:
   ```bash
   ls /usr/share/icons/ | grep -i "icon-theme"
   ```

2. Убедитесь, что название темы значков в settings.ini совпадает точно.

3. Обновите кэш значков:
   ```bash
   sudo gtk-update-icon-cache /usr/share/icons/theme-name/
   ```

### Проблемы с отображением шрифтов

1. Установите дополнительные пакеты шрифтов:
   ```bash
   sudo pacman -S freetype2 fontconfig
   ```

2. Проверьте настройки fontconfig:
   ```bash
   fc-match "sans-serif"
   ```

3. Очистите кэш шрифтов и пересоздайте его:
   ```bash
   fc-cache -fv
   ```

### Применение настроек ко всем приложениям

Некоторые приложения могут не сразу отражать настройки GTK. Это может происходить с:

- Приложениями Electron (VS Code, Discord и т.д.)
- Приложениями Qt (если не настроена соответствующая интеграция GTK)
- Приложениями, использующими собственную тему

Для приложений Qt рассмотрите возможность установки и настройки qt5-styleplugins и qt6-styleplugins для лучшей интеграции с темами GTK.

## Специфика настройки для Arch + Niri

Отлично! Давайте зафиксируем это «боевое» состояние. Когда всё работает на Arch так же, как на Gentoo, это идеальный момент для составления шпаргалки.

Главная проблема была в том, что GTK4 (Nautilus) и GTK3 (Pavucontrol) по-разному читают конфиги, а Libadwaita в Niri пытается найти GNOME-окружение и, не находя его, сыпет ошибками импорта.

### Документация по настройке GTK 3/4 (Arch + Niri)

#### 1. Глобальные настройки (GSettings)

GTK4 приложения (Nautilus) игнорируют settings.ini. Чтобы они стали темными, нужно прописать это в базе данных dconf:

```bash
# Включает предпочтение темной темы для Libadwaita
gsettings set org.gnome.desktop.interface color-scheme 'prefer-dark'

# Устанавливает базовую тему (лучше держать Adwaita, чтобы избежать ошибок импорта)
gsettings set org.gnome.desktop.interface gtk-theme 'Adwaita'
```

#### 2. Переменные окружения

В конфиге Niri (или .zprofile) должны быть эти строки, чтобы порталы и темы работали корректно:

* `export XDG_CURRENT_DESKTOP=GNOME` — заставляет GTK-приложения «чувствовать себя дома».
* `unset GTK_THEME` — важно! Переменная не должна быть задана, чтобы приложения читали локальные конфиги из ~/.config/.

#### 3. Структура файлов ~/.config/gtk-4.0/

Эта папка отвечает за современные приложения (Nautilus).

| Файл | Описание | Содержимое / Ссылка |
|---|---|---|
| noctalia.css | Твоя цветовая палитра | Твой кастомный CSS с @define-color |
| gtk.css | Точка входа | @import url("noctalia.css"); |
| gtk-dark.css | Темы оформления | Симлинк на /usr/share/themes/adw-gtk3/gtk-4.0/gtk-dark.css |
| settings.ini | Совместимость | gtk-application-prefer-dark-theme=1 |

> Важно: Если видишь ошибки Failed to import libadwaita.css, создай пустые файлы-заглушки в этой папке:
> ```bash
> touch ~/.config/gtk-4.0/libadwaita.css
> ```

#### 4. Структура файлов ~/.config/gtk-3.0/

Эта папка отвечает за классические приложения (Pavucontrol, Inkscape).

| Файл | Описание | Содержимое / Ссылка |
|---|---|---|
| noctalia.css | Копия палитры | Файл с цветами |
| gtk.css | Применение цветов | Симлинк на noctalia.css |
| settings.ini | Основная тема | gtk-theme-name=adw-gtk3 |
| bookmarks | Закладки Nautilus | touch ~/.config/gtk-3.0/bookmarks (чтобы не было ошибок в логах) |

#### 5. Почему это теперь работает?

* Иерархия: gtk.css подгружает цвета Noctalia поверх стандартной Adwaita.
* Симлинки: Твой gtk-dark.css теперь ссылается на системный конфиг adw-gtk3, который правильно переопределяет сложные переменные (headerbar, sidebar) для темного режима.
* GTK3/4 разделение: У GTK3 теперь есть свой gtk.css (через симлинк на noctalia), поэтому Pavucontrol подхватывает те же цвета, что и Nautilus.

#### Чек-лист при «поломке» темы в будущем:

* Выполните `echo $GTK_THEME` — если не пусто, ищи, кто её экспортирует.
* Проверьте симлинк gtk-dark.css — живой ли он (не удалил ли ты пакет adw-gtk3).
* Запустите `GTK_DEBUG=interactive nautilus` и посмотрите первую строку ошибок — она всегда скажет, какой именно файл не удалось прочитать.

Хочешь, я помогу составить небольшой скрипт-бэкапер, который будет одной командой упаковывать эти конфиги в архив или переносить их на другую систему?

## Проверка настроек

После настройки рекомендуется проверить работу приложений GTK разных версий:

1. Запустите приложение GTK4 (например, Nautilus):
   ```bash
   GTK_DEBUG=interactive nautilus
   ```

2. Запустите приложение GTK3 (например, pavucontrol):
   ```bash
   pavucontrol
   ```

3. Проверьте значения настроек:
   ```bash
   gsettings list-recursively | grep -i theme
   ```

4. Проверьте переменные окружения:
   ```bash
   env | grep -E "(GTK|XDG)"
   ```

## Дополнительные замечания

- Изменения в `/etc/gtk-3.0/settings.ini` влияют на всех пользователей системы
- Пользовательские настройки в `~/.config/gtk-3.0/settings.ini` переопределяют системные настройки
- Приложения GTK-2 используют другие методы конфигурации (обычно ~/.gtkrc-2.0)
- Некоторые среды рабочего стола (GNOME, KDE) имеют свои собственные системы темизации, которые могут переопределять настройки GTK
- Для достижения наилучших результатов убедитесь, что настройки темы среды рабочего стола совместимы с вашими настройками GTK