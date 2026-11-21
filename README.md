- 🎮 **Play Online (GitHub Pages)**: [https://karpenter0.github.io/sbr-mahjong/](https://karpenter0.github.io/sbr-mahjong/)
- ⬇️ **Download Offline Version (v1.0.0)**: [Download mahjong.html](https://github.com/karpenter0/sbr-mahjong/releases/download/v1.0.0/mahjong.html)

# Sichuan Mahjong (Sichuan Bloody Rules)

This is an offline desktop **四川麻将（血战到底·换三张）单机HTML游戏** |Sichuan Mahjong (*Sichuan Bloody Rules*, *Swap Three Tiles*) game. It is completely free, requires no registration or login, works offline with no ads, requests zero permissions, and collects no data—just open and play. Perfect for a quick solo break or sharpening your skills.

You play against three "AI" opponents powered by Depth-First Search (DFS) and a suite of heuristic algorithms rather than modern generative AI models. Every deal uses a truly pure and fair random shuffle with zero programmatic or manual tampering. Just like a human player, each bot can only see its own hand, all players' open melds, and the discards on the table—it has no access to other players' concealed hands or the remaining wall, relying purely on visible information for deduction and probability estimation. Bots operate independently and never share data with one another.

When the **"Future Pong/Kong Valuation"** toggle is enabled, the algorithm evaluates potential future Pong/Kong opportunities and assigns corresponding values whenever a Pong/Kong is available or when choosing a tile to discard after drawing. This expands the algorithm's search paths and decision options, typically adding 2–3 seconds (and occasionally over 10 seconds) per turn. If you prefer faster turns over this extra calculation, feel free to turn it off—even when disabled, you likely won't notice any drop in playing strength.

Version 1.0 supports customizable game settings. Rules are locked in once a match starts, and any changes take effect in the next match. All settings are saved locally in your browser.

---

## Scoring Rules

This game follows **Sichuan Mahjong (Sichuan Bloody Rules)**. Scoring starts with a base of 1 point and doubles for each Fan (*multiplier*). If your hand pattern plus winning condition totals $n$ Fan, you collect $2^n$ points ($1, 2, 4, 8, 16, 32, 64, 128, 256, 512, 1024\dots$) with no upper cap.

### Hand Patterns
* **Common Hand (Chicken Hand / *Pihu*)**: 0 Fan
* **All Pongs (*Duiduihu*)**: 1 Fan
* **Pure One Suit (*Qingyise*)**: 2 Fan
* **Seven Pairs (*Qidui*)**: 2 Fan
* **Dragon Seven Pairs (*Long Qidui*)**: 3 Fan (more intuitively understood as Seven Pairs [2 Fan] + 1 Root/*Gen* [1 Fan]); each additional Root (*Gen*) adds 1 Fan.

In addition to the standard patterns above, the following patterns are included:
* **All Simples / Middle Tiles (*Zhongzhang*, tiles 2–8 only)**: 1 Fan
* **All Terminals and Honors / Outside Hand (*Quandaiyao*, every meld/pair contains a 1 or 9)**: 2 Fan
* **Pure Terminals (*Quanyaojiu*, every single tile is a 1 or 9—meaning Dragon Seven Pairs is the only valid pattern)**: 3 Fan
* **All 2-5-8 (*Quanjiang*, every tile is 2, 5, or 8)**: 2 Fan
* **Pure Straight (*Yitiaolong*, 1–9 of the same suit)**: 2 Fan

Compatible patterns stack their Fan values (e.g., Pure One Suit + Seven Pairs + All Simples, Pure One Suit + Pure Straight, Pure One Suit + All Pongs + All Simples, Pure One Suit + Outside Hand). Incompatible patterns take the highest applicable Fan. **All 2-5-8** always stacks with **All Pongs (+1 Fan)** and **All Simples (+1 Fan)**.

### Winning Conditions
* **Single Wait after Full Meld (*Jingoudiao*)**, **Last Tile Draw (*Haidilao*)**, **Last Tile Discard (*Haidipao*)**, **Robbing the Kong (*Qianggang*)**, **Win on Kong Draw (*Gangshanghua*)**, and **Win on Kong Discard (*Gangshangpao*)** each add **1 Fan**.
* By default, **Self-Drawn (*Zimo*)** and **Concealed Hand (*Menqing*)** each add **1 Fan** (can be disabled or adjusted in settings).
* By default, **Win on Kong Draw after a Melded Kong (*Dianganghua*)** is paid equally by all un-won players.
* **Seven Pairs** naturally qualifies as a **Concealed Hand**.

### Configurable Rules
* **All Simples**, **Outside Hand / Pure Terminals**, **All 2-5-8**, **Pure Straight**, **Self-Drawn**, and **Concealed Hand** can each be configured individually.
* **Outside Hand** and **Pure Terminals** share a single toggle; Pure Terminals always awards 1 Fan more than Outside Hand, and the two do not stack. Optional Fan values can be set from **0 to 4 Fan** (with Pure Terminals automatically scaling to Outside Hand + 1 Fan).
* **Heavenly Hand (*Tianhu*)**, **Earthly Hand (*Dihu*)**, **Squeeze Five (*Jiaxinwu*)**, and **Pinned Two Bamboo (*Ka Ertiao*)** are disabled by default:
  * **Heavenly Hand**: The dealer wins directly on their initial hand right after swapping three tiles and declaring their void suit. Declaring a concealed Kong and drawing a replacement tile before winning does **not** count as Heavenly Hand.
  * **Earthly Hand**: A non-dealer wins by self-draw immediately on their very first normal draw, provided they have not called Pong or Kong beforehand (other players' Pong/Kong calls do not affect this). Declaring a concealed Kong after the first draw and winning on the replacement tile does **not** count as Earthly Hand.
  * Both Heavenly Hand and Earthly Hand stack with Concealed Hand, and Self-Drawn Fan is applied according to your settings.
* **Squeeze Five** requires waiting exclusively on a `5` of a suit and winning as the middle tile of a `4-5-6` sequence. **Pinned Two Bamboo** requires waiting exclusively on the `2 of Bamboo` and winning as the middle tile of a `1-2-3 of Bamboo` sequence.
* **Ready-Hand (*Tingpai*) Check**: Excludes any winning tile where all four copies are held in your own concealed hand (tiles in Pongs, exposed Kongs, or concealed Kongs do not trigger this exclusion). End-of-round penalty checks (*Cha Dajiao*) follow the exact same rule.
* **Win on Melded Kong Draw (*Dianganghua*)**: Configurable so that either all un-won players pay equally, or only the player who discarded into the Kong pays a single share (no full-liability payout). Both modes count as a self-drawn win; whether an extra Self-Drawn Fan is added depends on your Self-Drawn setting.
* *Note: Seven Connected Pairs (*Lian Qidui*) and Nine Gates (*Jiulian Baodeng*) are not currently supported.*

### Timely Rain (*Jishiyu*)
* Disabled by default. When enabled, a **Promoted Kong (*Bugang*)** only collects Kong points if declared immediately upon drawing the fourth copy of a previously Ponged tile. If you already held the fourth copy when calling Pong, or failed to declare the Kong immediately upon drawing it, promoting the Kong later awards no Kong points.
* Exposed Kongs (*Zhigang*), Concealed Kongs (*Angang*), Robbing the Kong, Win on Kong Draw, Win on Kong Discard, and Root (*Gen*) rules remain unaffected.

---

## Single-File Build

With **Node.js 18+** installed, run the following commands in the project root directory:

```bash
npm install
npm run build:single
```

During mobile adaptation development, this command generates `dist/mahjong-mobile-preview.html`, bundling the game logic, styles, 34 tile graphics, and sound effects into a single file. Re-running the command overwrites the preview file without affecting the existing `dist/mahjong.html`.

---

## Author & License

* **Author**: karpenter0
* **Contact**: karpenter0@gmail.com
* **License**: [MIT License](LICENSE)
