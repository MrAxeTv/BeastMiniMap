# Languages and Messages

BeastMiniMap uses one server-wide language. Player/admin messages, map controls, tooltips and dialogs are editable under `plugins/BeastMiniMap/Lang/`.

Select a file in `config.yml`, then run `/beastminimap reload`:

```yaml
Options:
  Language:
    Settings:
      File: en-US.yml
      AutoDownload: true
      ForceLanguage: false
```

`ForceLanguage` is reserved; it does not enable per-player locale selection. English (`en-US.yml`) is the default and remains available offline.

## Bundled and Optional Languages

There are 50 maintained translations: 33 bundled and 17 optional [official downloads](https://github.com/MrAxeTv/BeastMiniMap/tree/main/languages).

| File | Language | Included |
| --- | --- | --- |
| `ar.yml` | Arabic | Optional |
| `bg.yml` | Bulgarian | Bundled |
| `bs.yml` | Bosnian | Bundled |
| `ca.yml` | Catalan | Bundled |
| `cs.yml` | Czech | Bundled |
| `da.yml` | Danish | Bundled |
| `de.yml` | German | Bundled |
| `el.yml` | Greek | Bundled |
| `en.yml` | English | Optional |
| `en-GB.yml` | English (United Kingdom) | Optional |
| `en-US.yml` | English (United States; default) | Bundled |
| `es.yml` | Spanish | Bundled |
| `et.yml` | Estonian | Bundled |
| `eu.yml` | Basque | Bundled |
| `fi.yml` | Finnish | Bundled |
| `fil-PH.yml` | Filipino (Philippines) | Optional |
| `fr.yml` | French | Bundled |
| `ga-IE.yml` | Irish (Ireland) | Bundled |
| `gv-IM.yml` | Manx (Isle of Man) | Bundled |
| `he.yml` | Hebrew | Optional |
| `hi-IN.yml` | Hindi (India) | Optional |
| `hr.yml` | Croatian | Bundled |
| `hu.yml` | Hungarian | Bundled |
| `is-SV.yml` | Icelandic (filename alias) | Bundled |
| `it.yml` | Italian | Bundled |
| `ja.yml` | Japanese | Optional |
| `ko.yml` | Korean | Optional |
| `lol-US.yml` | Playful English (LOLCAT) | Optional |
| `lt.yml` | Lithuanian | Bundled |
| `lv-LV.yml` | Latvian (Latvia) | Bundled |
| `mn-MN.yml` | Mongolian (Mongolia) | Optional |
| `nl.yml` | Dutch | Bundled |
| `no.yml` | Norwegian | Bundled |
| `pl.yml` | Polish | Bundled |
| `pt.yml` | Portuguese | Bundled |
| `pt-BR.yml` | Portuguese (Brazil) | Optional |
| `ro.yml` | Romanian | Bundled |
| `ru.yml` | Russian | Bundled |
| `si-LK.yml` | Sinhala (Sri Lanka) | Optional |
| `sk.yml` | Slovak | Bundled |
| `sr.yml` | Serbian (Latin) | Bundled |
| `sr-CS.yml` | Serbian (Cyrillic) | Bundled |
| `sv.yml` | Swedish | Bundled |
| `th.yml` | Thai | Optional |
| `tr.yml` | Turkish | Bundled |
| `uk.yml` | Ukrainian | Bundled |
| `vi.yml` | Vietnamese | Optional |
| `zh.yml` | Chinese (Simplified) | Optional |
| `zh-HK.yml` | Chinese (Traditional, Hong Kong) | Optional |
| `zh-TW.yml` | Chinese (Traditional, Taiwan) | Optional |

Use these filenames exactly. `is-SV.yml` is the supported Icelandic alias. Translations are machine-assisted and can be adjusted by administrators.

Only English and the selected file are created in `Lang/`. With `AutoDownload: true`, selecting an optional locale fetches only that official file from the language snapshot matching the plugin build. Size and SHA-256 are checked. Existing customized values/comments are preserved; English is used while a download is pending or unavailable.

For manual installation, download the matching language YAML into `Lang/`, select its filename and reload. `AutoDownload: false` disables automatic fetching without disabling installed optional or custom files. Resource-pack artwork downloads are separate and remain manual.

## Customize Text

Copy `en-US.yml` to a new filename for a custom translation. Translate values while preserving keys, command IDs and named placeholders such as `{player}` and `{limit}`. Missing entries fall back to English; reload preserves customized existing entries.

To change the framed atlas title in the selected language file:

```yaml
Gui:
  Atlas:
    Title: "MY SERVER ATLAS"
```

Keep this title Latin and short; the header fits up to 35 bitmap characters. An empty value hides it.

## Pixel Font and Native Menus

Chat and native dialogs support Unicode. The compact pixel font normalizes accented Latin but cannot display every script. For Russian, Greek, Arabic, Hebrew and Asian scripts, use:

```yaml
Atlas:
  MenuUi: native
```

The atlas frame/header still uses its compact bitmap font, so retain Latin text there. Changing language does not add fonts or require a resource-pack rebuild.

Trusted language values accept MiniMessage and Beast-style color formatting. Keep menu labels short enough for their controls. Dynamic player names and other substituted values are inserted as literal text.
