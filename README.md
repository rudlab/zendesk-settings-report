# zendesk-settings-report

Sjálfvirkt uppfærð yfirlitssíða yfir Zendesk stillingar Háskóla Íslands.

## 🌐 [rudlab.github.io/zendesk-settings-report](https://rudlab.github.io/zendesk-settings-report/)

Síðan sýnir gagnvirkt flæðiskema: hvaða þjónustunetföng HÍ fara í hvaða þjónustuhópa í Zendesk, og hvaða triggerar stýra því flæði.

---

## Hvað er sýnt

**Vinstri dálkur** — þjónustunetföng (`gjaldkeri@hi.is`, `help@hi.is`, o.fl.)  
**Hægri dálkur** — þjónustuhópar (`FJSV gjaldkerar`, `UTS Tölvuþjónusta`, o.fl.)  
**Línur á milli** — tengingar stýrðar af Zendesk triggers

Smelltu á netfang eða hóp til að:
- sjá allar tengingar þess
- skoða META trigger (setur tag) og ROUTE trigger (úthlutar hóp)

## Uppfærsla

Síðan uppfærist sjálfkrafa **á hverjum degi kl. 06:00 UTC** af [`rudlab/zendesk-settings-sniffer`](https://github.com/rudlab/zendesk-settings-sniffer).

Tíminn „Stillingar sóttar" efst til hægri á síðunni sýnir hvenær gögnin voru sótt.

## Uppbygging flæðisins

```
recipient: gjaldkeri@hi.is
      │
      ▼  [CREATE][META][FJSV] – Classify source gjaldkeri
      │   → setur tag:  meta_fjsvgjaldkeri
      │
      ▼  [CREATE][ROUTE][FJSV] – Route to FJSV gjaldkeri
           → úthlutar á: FJSV gjaldkerar (group_id: 43976195331611)
```

META-triggerar lesa `recipient` og setja `meta_*` tag.  
ROUTE-triggerar lesa `meta_*` tag og setja `group_id`.

## Tenglar

- ⚙️ Sniffer repo (private): [github.com/rudlab/zendesk-settings-sniffer](https://github.com/rudlab/zendesk-settings-sniffer)
- 🔧 Zendesk Admin: [haskoliislands.zendesk.com/admin](https://haskoliislands.zendesk.com/admin)
