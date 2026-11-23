# 🎮 ScarZero Game Store

> A desktop game store and admin management system built in Python with CustomTkinter, featuring separate customer and administrator applications over a shared file-based data layer.

[![Python](https://img.shields.io/badge/Python-3.14%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![CustomTkinter](https://img.shields.io/badge/CustomTkinter-5.2.2-333333?logo=github)](https://github.com/TomSchimansky/CustomTkinter)
[![Course](https://img.shields.io/badge/Course-CSE101-yellow)](https://ece.northsouth.edu/courses/cse101-introduction-to-python-programming/)
[![NSU](https://img.shields.io/badge/NSU-North%20South%20University-1E90FF)](https://www.northsouth.edu/)

[![Platform](https://img.shields.io/badge/platform-windows%20%7C%20linux%20%7C%20macos-brightgreen)](#-quick-start)
[![License](https://img.shields.io/badge/license-custom--non--commercial-orange)](#-license)
[![Repository](https://img.shields.io/badge/GitHub-GameStore--Python-333333?logo=github)](https://github.com/sifat-jaman-13/GameStore-Python)

---

## 📚 Project Information

| Field | Value |
|-------|-------|
| **Project** | ScarZero Game Store |
| **Author** | Sifat Jaman |
| **Course** | CSE101 — Introduction to Python Programming |
| **Institution** | North South University |
| **Type** | Solo project |
| **Language** | Python 3.14+ |
| **GUI Framework** | CustomTkinter 5.2.2 |
| **Size** | 39 Python files, ~3,500 lines of code |
| **Repository** | [sifat-jaman-13/GameStore-Python](https://github.com/sifat-jaman-13/GameStore-Python) |

---

## 🎯 Overview

ScarZero Game Store is a two-application desktop system: a **customer storefront** where users register, browse a game catalogue, manage a cart and wallet, and build a library of purchases; and an **admin console** where an administrator manages the catalogue, users, and incoming requests.

Both applications share one data layer — pipe-separated text files in `GameStoreApp/data/` — so changes made in the admin console are visible in the storefront on the next read.

The project demonstrates modular package design, separation of GUI from data access, input validation, and file-based persistence without an external database.

---

## ✨ Features

### Customer Application (`GameStoreApp/main.py`)

Seven sections, presented as tabs:

| Tab | Capability |
|-----|-----------|
| **Home** | Welcome view with a curated list of highlighted titles |
| **Store** | Browse the catalogue, free-text search, filter by category |
| **Library** | View games already purchased |
| **Cart** | Add and remove games before checkout |
| **Wallet** | View balance and submit top-up requests for admin approval |
| **Profile** | View account details and submit change requests for approval |
| **Messages** | Support conversation with the administrator |

Plus registration and login with input validation.

### Admin Console (`run_admin.py`)

Seven sections, presented as tabs:

| Tab | Capability |
|-----|-----------|
| **Dashboard** | Overview cards for games, users, and support activity |
| **Games** | Add, edit, and delete games; manage categories |
| **Users** | View accounts and change status (active / disabled / banned) |
| **Wallet Requests** | Approve or reject customer top-up requests |
| **Profile Requests** | Approve or reject customer profile changes |
| **Messages** | Read and reply to customer support messages |
| **Settings** | Change the stored admin username and password |

Admin login is limited to 5 attempts; the counter persists across view changes.

---

## 📋 Requirements

| Requirement | Minimum |
|-------------|---------|
| **OS** | Windows 10+, Linux (Ubuntu 20.04+), macOS 10.13+ |
| **Python** | 3.14 or higher |
| **RAM** | 512 MB |
| **Disk** | ~100 MB including the virtual environment |

### Dependency

```
customtkinter~=5.2.2
```

That is the project's only third-party dependency. Everything else is Python's standard library. On Linux, `tkinter` must also be present at the system level — see [Troubleshooting](#-troubleshooting).

### Verify your toolchain

```bash
python --version
```

---

## 🚀 Quick Start

### Windows

```bash
git clone https://github.com/sifat-jaman-13/GameStore-Python.git
cd GameStore-Python
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

### Linux / macOS

```bash
git clone https://github.com/sifat-jaman-13/GameStore-Python.git
cd GameStore-Python
chmod +x setup_linux.sh
./setup_linux.sh
source .venv/bin/activate
```

Or manually:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
```

For a detailed Linux walkthrough, see [LINUX_SETUP.md](LINUX_SETUP.md).

---

## 🖥️ Usage

Activate the virtual environment first, then launch either application.

### Admin console

```bash
python run_admin.py
```

### Customer storefront

```bash
python GameStoreApp/main.py
```

Both entry points insert the correct directories onto `sys.path`, so they can be run from the project root.

On first launch, `init_db()` creates any missing data files in `GameStoreApp/data/`.

---

## 🔐 Default Credentials

### Admin console

```
Username: Sifat
Password: 1313
```

Defined in [`GameStoreApp/config.py`](GameStoreApp/config.py) and overridable from the console's **Settings** tab, which writes to `data/admin.txt`.

### Demo customer accounts

`data/users.txt` ships with 18 demo accounts. The primary one is:

```
Username: sifat13
Password: 1313
```

The remaining 17 use the password `1234`. All demo contact details are placeholders.

> ⚠️ **Security note:** credentials are stored in plain text, which is acceptable for a coursework demonstration but not for production. A real deployment needs salted password hashing (for example `bcrypt` or `argon2`).

---

## 📁 Project Structure

```
GameStore-Python/
├── run_admin.py                    # Admin console entry point
├── requirements.txt                # Python dependencies
├── setup_linux.sh                  # Linux/macOS setup script
├── LINUX_SETUP.md                  # Detailed Linux guide
├── TEST_REPORT.md                  # Cross-platform test report
├── LICENSE                         # Proprietary non-commercial use licence
├── ScarZero_Game_Store_Project_Summary.docx
└── GameStoreApp/
    ├── main.py                     # Customer storefront entry point
    ├── config.py                   # Titles, window size, admin defaults
    ├── auth/
    │   ├── login.py                # Customer login
    │   ├── register.py             # Customer registration
    │   ├── admin_login.py          # Admin login with attempt limiting
    │   └── validation.py           # Input validation helpers
    ├── admin/
    │   ├── admin_dashboard.py      # Admin shell and tab container
    │   ├── manage_games.py         # Game and category management
    │   ├── manage_users.py         # User account management
    │   ├── wallet_requests.py      # Wallet top-up approvals
    │   ├── profile_requests.py     # Profile change approvals
    │   ├── admin_messages.py       # Support message management
    │   └── admin_settings.py       # Admin credential changes
    ├── user/
    │   ├── dashboard.py            # Customer shell and tab container
    │   ├── store.py                # Catalogue browsing, search, filter
    │   ├── cart.py                 # Shopping cart
    │   ├── library.py              # Purchased games
    │   ├── wallet.py               # Balance and top-up requests
    │   ├── profile.py              # Profile view and change requests
    │   └── messages.py             # Support conversation
    ├── core/
    │   ├── file_handler.py         # Read/write pipe-separated tables
    │   ├── constants.py            # File paths and separator
    │   ├── catalog.py              # Catalogue queries
    │   ├── session.py              # Logged-in user state
    │   ├── admin_credentials.py    # Admin credential storage
    │   ├── message_utils.py        # Message threading helpers
    │   └── utils.py                # Shared utilities
    ├── ui/
    │   ├── theme.py                # Colour and font theme
    │   ├── styles.py               # Styling helpers
    │   └── components.py           # Reusable widgets
    ├── data/                       # Pipe-separated data files
    └── assets/                     # Application assets
```

---

## 🏗️ Architecture

The codebase is organised into five packages with one responsibility each:

- **`auth/`** — entry gates. Validates input and hands a session to the dashboards.
- **`admin/` and `user/`** — the two GUI trees. Each has a shell module that owns a tab container, plus one module per tab.
- **`core/`** — all data access. GUI modules never open files directly; they call `file_handler.read_table()` and `write_table()`, which keeps the storage format in one place.
- **`ui/`** — theming and reusable widgets, so visual changes happen in one location.

`Session` holds the logged-in user, and controllers are passed down to child frames so navigation and shared state stay explicit rather than global.

---

## 💾 Data Persistence

Data lives in pipe-separated (`|`) text files under `GameStoreApp/data/`. `init_db()` creates any that are missing on startup.

### Tracked seed data

| File | Contents |
|------|----------|
| `games.txt` | 62 games — id, title, genre, price, stock, developer, publisher, studio, year |
| `categories.txt` | 35 category names |
| `users.txt` | 18 demo accounts — username, password, email, phone, display name, status, balance |

### Runtime files (git-ignored, created on demand)

`admin.txt` · `cart.txt` · `purchases.txt` · `messages.txt` · `message_sessions.txt` · `message_status.txt` · `profile_requests.txt` · `wallet_requests.txt`

These hold per-run state rather than project content, so they are excluded from version control and regenerated automatically.

> **Note:** plain text is used deliberately, to keep the storage layer readable for coursework. A production system would use SQLite or PostgreSQL.

---

## 🐛 Troubleshooting

**`python` is not recognised**
Ensure Python is on your `PATH`. On Linux and macOS use `python3`.

**Virtual environment will not activate**
Use `.venv\Scripts\activate` on Windows and `source .venv/bin/activate` on Linux/macOS. Your prompt should show `(.venv)`.

**`ModuleNotFoundError: No module named 'customtkinter'`**
The virtual environment is not active, or dependencies were not installed. Activate it, then run `pip install --upgrade -r requirements.txt`.

**GUI fails to start on Linux (`no module named _tkinter`)**
Install Tk at the system level:

```bash
sudo apt-get install python3-tk python3-dev   # Debian / Ubuntu
sudo dnf install python3-tkinter              # Fedora
sudo pacman -S tk                             # Arch
```

**Permission denied running `setup_linux.sh`**

```bash
chmod +x setup_linux.sh
```

**Data files not found or not saving**
`GameStoreApp/data/` must be writable. The files are created automatically on first launch.

---

## ⚠️ Known Limitations

1. Passwords are stored in plain text, not hashed.
2. No database — concurrent writes from both applications running at once can overwrite each other.
3. Store search is a single free-text match plus a category filter; there is no filtering by price range or developer.
4. There is no review or rating system.
5. The admin **Dashboard** tab shows summary counts only, not historical analytics or reports.
6. Data files are read in full on each access, which would not scale past a few thousand rows.
7. No automated test suite; verification was manual and is recorded in [TEST_REPORT.md](TEST_REPORT.md).

---

## 🗺️ Roadmap

- [ ] Hash passwords with `bcrypt` or `argon2`
- [ ] Migrate the storage layer to SQLite behind the existing `file_handler` interface
- [ ] Add price-range and developer filters to the store
- [ ] Add a review and rating system
- [ ] Expand the admin dashboard into real sales reporting
- [ ] Add a `pytest` suite covering `core/`
- [ ] Package as a standalone executable with PyInstaller

---

## 🎓 Learning Outcomes

- **Package design** — a multi-package application with clear responsibility boundaries
- **GUI development** — event-driven interfaces with CustomTkinter
- **Separation of concerns** — GUI code isolated from the data-access layer
- **File I/O** — designing and parsing a delimited storage format
- **State management** — sessions and controller passing across views
- **Input validation** — guarding every user-supplied field
- **Cross-platform development** — one codebase on Windows, Linux, and macOS

---

## 👤 Author

**Sifat Jaman** — [@sifat-jaman-13](https://github.com/sifat-jaman-13)
North South University, Department of Electrical and Computer Engineering

### Related project

[**Movie-Project-Java**](https://github.com/sifat-jaman-13/Movie-Project-Java) — the same store architecture rebuilt in Java 17 with JavaFX, for CSE215.

---

## 📜 License

This project is available under a **proprietary non-commercial use licence**. Individual personal and educational use is permitted under the terms in [LICENSE](LICENSE). Commercial or organisational use requires prior written permission.
