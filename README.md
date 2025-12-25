<p align="center">
  <img src="dns_logo.jpg" alt="BIND" width="300">
</p>

## ![Lesson](https://img.shields.io/badge/Lesson-DNS_Split--DNS-00758F?style=for-the-badge&logo=linux&logoColor=white&labelColor=111827)![Author](https://img.shields.io/badge/Author-Kamil%20Ibragimov-10B981?style=for-the-badge&logo=github&logoColor=white&labelColor=111827)![Date](https://img.shields.io/badge/Date-25.12.2025-F59E0B?style=for-the-badge&logo=calendar&logoColor=white&labelColor=111827)

### 📌 Задание
1. Поднять стенд на CentOS 7 (2 сервера, 2 клиента).
2. Настроить зону `dns.lab`.
3. Добавить зону `newdns.lab` с записью `www`.
4. Настроить **Split-DNS**:
   - **client1** видит `web1.dns.lab` и `newdns.lab`.
   - **client2** видит полную зону `dns.lab`, но не видит `newdns.lab`.

### ✅ Результат
- [x] Стенд разворачивается через `vagrant up`.
- [x] Split-DNS работает (проверено через `ping` и `dig`).

---

## 🧰 Шаг 1 — Инфраструктура
Схема сети:
| Хост | IP | Роль |
|------|----|------|
| **ns01** | 192.168.50.10 | Master DNS |
| **client** | 192.168.50.15 | Client 1 |
| **client2** | 192.168.50.16 | Client 2 |

---

## 🧰 Шаг 2 — Запуск
Просто запускаем Vagrant:
```bash
vagrant up
```

---

## 🧰 Шаг 3 — Проверка

### 1. Проверка с Client 1 (192.168.50.15)
```bash
vagrant ssh client
ping -c 2 web1.dns.lab      # Работает
ping -c 2 web2.dns.lab      # Ошибка (скрыто через view)
ping -c 2 www.newdns.lab    # Работает
```

### 2. Проверка с Client 2 (192.168.50.16)
```bash
vagrant ssh client2
ping -c 2 web1.dns.lab      # Работает
ping -c 2 web2.dns.lab      # Работает
ping -c 2 www.newdns.lab    # Ошибка (зона не прописана в view)
```

**Результаты тестов подтверждают корректную работу Split-DNS согласно ТЗ.**
