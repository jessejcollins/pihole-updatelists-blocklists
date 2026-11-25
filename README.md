# Supplemental DNS Block Lists

This repo holds two files for Pi-hole:

| File | Purpose |
| --- | --- |
| [`blocklists.txt`](blocklists.txt) | Every adlist URL Pi-hole uses, one per line. [pihole-updatelists](https://github.com/jacklul/pihole-updatelists) reads it in place of the [Firebog "ticked" list](https://v.firebog.net/hosts/lists.php?type=tick). |
| [`list.txt`](list.txt) | A small hosts-format blocklist of domains that other lists missed in [d3ward's Adblock Test](https://d3ward.github.io/toolz/adblock.html). It is one of the entries in `blocklists.txt`. |

## `blocklists.txt`

This is the single source of truth for Pi-hole's adlists; none are managed by hand in the Pi-hole UI. It replaces the Firebog ticked list, which pulled in many lists that duplicate larger aggregated lists, plus at least one dead list (URLhaus, which now returns HTTP 410).

### Compose setting

```yaml
BLOCKLISTS_URL: 'https://raw.githubusercontent.com/jessejcollins/supplement_firebog_dns_block_list/main/blocklists.txt'
```

pihole-updatelists **disables** lists that drop out of this file but does not delete them; delete those in the Pi-hole UI. With the default `REQUIRE_COMMENT=true`, it only manages adlists whose comment contains `Managed by pihole-updatelists`, so an adlist added by hand is ignored even if its URL is in this file.

### Included

- **Main aggregated lists:** HaGeZi Pro, OISD Big
- **HaGeZi add-ons:** Threat Intelligence Feeds (`tif`), DGA domains (30 days, from the NRD repo), badware hoster, dynamic DNS, spam TLDs, pop-up ads, fake
- **NSFW:** OISD NSFW, chadmayfield porn top 1M
- **Other malware:** cyberhost malware
- **From Firebog, not covered elsewhere:** StevenBlack unified hosts, Frogeye first-party trackers, WindowsSpyBlocker spy, Prigent-Crypto, AssoEchap stalkerware indicators
- **This repo:** `list.txt`

### Dropped from the Firebog set (already covered elsewhere)

- **In StevenBlack unified hosts:** AdAway, FadeMind add.Spam, add.2o7Net, add.Risk and UncheckyAds, KADhosts, pgl.yoyo.org, bigdargon hostsVN
- **In OISD Big:** w3kbl, Spam404
- **Sources for HaGeZi Multi/Pro:** Firebog AdguardDNS, Easylist and Easyprivacy, notrack-malware
- **Sources for HaGeZi TIF:** Phishing Army extended, DandelionSprout AntiMalwareHosts, URLhaus (dead)
- **Undecided, left out for now:** Firebog Admiral (probably in OISD), anudeepND adservers, Prigent-Ads
