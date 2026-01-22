# Word-Gen - High-Performance Wordlist Generator

**Word-Gen** is a powerful, memory-efficient wordlist generation utility designed for security professionals, penetration testers, and CTF players. It generates realistic password permutations based on base words by applying intelligent transformations.

## 🚀 Features

*   **Smart Permutations:** Automatically handles uppercase/lowercase variations and common leetspeak substitutions (e.g., 'a' -> '@', 'e' -> '3').
*   **Suffix Expansion:**
    *   **Numeric:** Appends all 1-4 digit combinations (0-9999).
    *   **Years:** Appends years from a custom range (e.g., 1980-2025) with optional 2-digit variations.
    *   **Custom:** Append static special characters or strings (e.g., '!').
*   **Multiple Inputs:** Process multiple base words in a single run.
*   **Size Estimation:** Instantly estimates the file size and line count before generation to prevent disk overflow.
*   **Streamed Output:** Uses Python generators for memory safety, capable of creating multi-gigabyte wordlists without eating RAM.
*   **Progress Tracking:** Real-time progress bar with rate calculation.

## 📋 Requirements

*   Python 3.6+

## 🛠️ Usage

```bash
python word-gen.py [options] [words...]
```

### Basic Examples

**Generate variants for a single word:**
```bash
python word-gen.py admin
```

**Generate variants for multiple words:**
```bash
python word-gen.py admin user root
```

**Save output to a file:**
```bash
python word-gen.py admin -o wordlist.txt
```

### Advanced Permutations

**Append simple numeric codes (0-9999):**
Useful for finding passwords like `Admin123`, `admin2022`.
```bash
python word-gen.py admin --append-digits
```

**Append years (e.g., birth years or significant dates):**
Generates `admin1990`, `Admin1991`...
```bash
python word-gen.py admin --years 1990-2024
```
*Add `--year2` to also include Short years (e.g., `90`, `91`).*

**Add a custom suffix (e.g., for complexity requirements):**
Generates `admin!`, `Admin@!`...
```bash
python word-gen.py admin --suffix "!"
```

**Combine everything:**
```bash
python word-gen.py companyname --append-digits --years 2020-2025 --suffix "!" -o target_list.txt
```

### Safety Features

**Check how massive the list will be without generating it:**
```bash
python word-gen.py admin -a -y 1900-2000 --count-only
```

**Limit the output:**
Stop after the first 1,000,000 lines.
```bash
python word-gen.py admin -a --limit 1000000
```

## 📝 Substitution Rules
The tool currently applies the following default substitutions:
*   **a**: a, A, @, 4
*   **b**: b, B, 8
*   **c**: c, C, (
*   **e**: e, E, 3
*   **g**: g, G, 9, 6
*   **i**: i, I, 1, !
*   **l**: l, L, 1, |
*   **o**: o, O, 0
*   **s**: s, S, $, 5
*   **t**: t, T, 7, +
*   **z**: z, Z, 2

## ⚖️ Disclaimer
This tool is intended for legal security auditing, penetration testing, and educational purposes only. The author allows its use only on systems where you have explicit permission to test coverage.

## 📜 License
Unlicensed / Open Source.
