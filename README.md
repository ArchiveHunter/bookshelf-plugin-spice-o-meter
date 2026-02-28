# 🌶️ Spice-o-Meter

A plugin for [Family Bookshelf](https://github.com/JokerJonno/family-bookshelf) that adds a separate heat level rating to every book, independent of the star rating. Perfect for dark romance readers who want to know exactly how spicy a book is before diving in.

---

## What it does

- **Book cards** — shows the average chilli rating at a glance
- **Book detail** — full spice rating section with per-reader ratings and an easy picker
- **Stats page** — heat distribution chart and a spiciest books leaderboard

## Rating scale

| Rating | Meaning |
|---|---|
| 🌶️ | Barely there — fade to black |
| 🌶️🌶️ | Warm — some steam but tasteful |
| 🌶️🌶️🌶️ | Hot — explicit but not overwhelming |
| 🌶️🌶️🌶️🌶️ | Very hot — frequent and detailed |
| 🌶️🌶️🌶️🌶️🌶️ | Scorching — this book is basically on fire |

---

## Installation

### Prerequisites
- [Family Bookshelf](https://github.com/JokerJonno/family-bookshelf) up and running

### Install

```bash
cd ~/bookshelf
git clone https://github.com/JokerJonno/bookshelf-plugin-spice-o-meter plugins/spice-o-meter
docker compose down && docker compose up -d --build
```

### Verify

Check the server logs for:
```
🔌 Plugin loaded: Spice-o-Meter (spice-o-meter) v1.0.0
```

### Uninstall

```bash
rm -rf ~/bookshelf/plugins/spice-o-meter
docker compose down && docker compose up -d --build
```

Your spice rating data remains in the SQLite database but is no longer active.

---

## How it works

The plugin adds a `spice_ratings` table to the shared SQLite database. Each reader can submit one chilli rating per book, which can be updated at any time. Ratings are stored independently of the main star ratings.

### API endpoints

All routes are prefixed with `/api/plugins/spice-o-meter/`

| Method | Path | Description |
|---|---|---|
| GET | `/book/:id` | Get spice ratings for a book |
| POST | `/book/:id` | Add or update a spice rating |
| GET | `/books` | Get average spice for all books (used by card display) |
| GET | `/stats` | Spiciest books and heat distribution |

---

## Plugin hooks

| Hook | Description |
|---|---|
| `bookCard` | Chilli display below star rating on each card |
| `bookDetail` | Full spice section in book detail modal |
| `stats` | Heat distribution chart and spiciest books widget |

---

## Part of the Family Bookshelf ecosystem

- 📚 [family-bookshelf](https://github.com/JokerJonno/family-bookshelf) — the core platform
- 🌶️ bookshelf-plugin-spice-o-meter — this plugin
- 🚫 [bookshelf-plugin-dnf-tracker](https://github.com/JokerJonno/bookshelf-plugin-dnf-tracker) — Did Not Finish tracker
