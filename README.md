# Кэширующий DNS-сервер

Простой кэширующий DNS-прокси сервер с поддержкой записей A, AAAA, NS и PTR.

## Особенности
- Кэширование всех типов DNS-записей
- Автоматическое обновление TTL
- Сохранение кэша на диск
- Поддержка рекурсивных запросов
- Логирование всех операций

## Требования
- Python 3.6+
- Права root для работы на порту 53

## Установка
1. Скопируйте файлы сервера:
server.py
utils.py

## Запуск

Базовый запуск (на порту 53):
```bash
sudo python3 server.py
```

```Bash
sudo python3 server.py \
  --upstream-dns 1.1.1.1 \
  --listen-port 5353 \
  --cache-ttl 600 \
  --backup-file custom_cache.bin
```

# Параметры командной строки

Параметр   По 
ВФВФ

| Параметр         | По умолчанию  | Описание                          |
|------------------|--------------|-----------------------------------|
| `--upstream-dns` | `8.8.8.8`    | Вышестоящий DNS-сервер            |
| `--upstream-port`| `53`         | Порт вышестоящего DNS             |
| `--listen-port`  | `53`         | Локальный порт прослушивания      |
| `--listen-addr`  | `0.0.0.0`    | Локальный адрес                   |
| `--cache-ttl`    | `300`        | Время жизни кэша (сек)            |
| `--backup-file`  | `dns_cache.bin` | Файл для хранения кэша           |

# Примеры использования

1. Простой тестовый запрос:
```bash
dig @127.0.0.1 google.com
```
2. Проверка кэширования (второй запрос должен быть быстрее):
```bash
dig @127.0.0.1 google.com 
```
3. Проверка разных типов записей:
```bash
dig @127.0.0.1 google.com AAAA
dig @127.0.0.1 google.com NS
```

#### 2. Тестирование

# Тестирование DNS-сервер

### 1. Базовый тест работы
```bash
dig @127.0.0.1 google.com
```
Ожидаемый результат:

- Ответ содержит IP-адреса Google
- В логах сервера: "Processing query: google.com"
