# YouTube Terminal (comandă: `yt`)

> © 2026 vatamanuvd. Toate drepturile rezervate.
> Acest script este creat și administrat de vatamanuvd.
> Orice redistribuire trebuie să păstreze acest căsuță de autor.
> Marcă: **YouTube Terminal** / **yt** (vatamanuvd) — nu revendica autoria altcineva.

---

## Ce este

`yt` (YouTube Terminal) este un script bash mic care îți permite să cauți și să redai
videouri YouTube **direct din terminal**, fără browser, la cea mai
bună calitate utilă (1080p60 H.264), folosind `yt-dlp` + `fzf` + `mpv`.

Creat de vatamanuvd pentru fluxul său de lucru pe Linux (Fedora + Sway),
ca parte din canalul său de YouTube despre Linux, self-hosting și homelab.

## De ce

- Îți păstrează atenția în terminal (nu deschizi browser).
- Calitate maximă fără auto-downgrade la 480p (problema clasică la
  ytfzf și la redarea brută yt-dlp).
- Funcționează pe Wayland/Sway (unde accelerația hardware video e fragilă):
  decodează software 1080p H.264, care rulează fluid pe orice CPU modern.

## Dependințe

- `yt-dlp` — instalat via `sudo dnf install yt-dlp`
- `mpv` — `sudo dnf install mpv`
- `fzf` — `sudo dnf install fzf`
- `deno` — runtime JavaScript necesar pentru extractorul YouTube 2026:
  `curl -fsSL https://deno.land/install.sh | sh` (se instalează în `~/.deno/bin`)

Config suplimentar recomandat (`~/.config/yt-dlp/config`):
```
--js-runtimes deno
--remote-components ejs:github
--format bv*+ba/best
```

## Instalare

1. Salvează scriptul `yt` în `~/bin/` și fă-l executabil:
   `chmod +x ~/bin/yt`
2. Asigură-te că `~/bin` e în PATH.
3. rulează o dată: `yt "lofi hip hop"` ca să confirmi că funcționează.

## Uz

| Comandă | Ce face |
|---------|---------|
| `yt "cautare"` | Caută pe YouTube, afișează o listă, alegi cu fzf, redă în mpv |
| `yt -n 10 "cautare"` | Caută 10 rezultate (implicit 20) |
| `yt <url>` | Redă direct un link YouTube la calitate maximă |

## Scurtături mpv (fără mouse)

| Tastă | Acțiune |
|-------|---------|
| `f` | Fullscreen pornit/oprit |
| `SPACE` | Play / Pause |
| `←` `→` | Salt înapoi / înainte 5 sec |
| `↑` `↓` | Volum mai tare / mai încet |
| `[` `]` | Mai încet / mai repede |
| `m` | Mute pornit/oprit |
| `q` | Ieșire (salvează poziția) |
| `Q` | Ieșire (fără salvare) |

## Cum funcționează (pe scurt)

1. Pentru o căutare: `yt-dlp` face un `ytsearchN:query` și returnează
   titlu | canal | durată | url.
2. Lista e afișată în `fzf` — alegi cu sus/jos + Enter.
3. `mpv` deschide video-ul cu formatul forțat la 1080p H.264
   (`bv*[height<=1080][vcodec~='(avc|h264|hevc|h265)']+ba/best`) și
   `--hwdec=no` (decode software, fără erori pe Wayland).
4. Pentru un URL direct: se sare direct la pasul 3.

## Note / limitări

- YouTube schimbă frecvent extractorul. Dacă `yt-dlp` dă eroare,
  rulează `yt-dlp -U` (auto-update).
- Codul sursă este versionat în acest repo (mirror public al lui
  vatamanuvd). Pentru codul complet de dotfiles vezi profilul autorului.

---

© 2026 vatamanuvd — creat de vatamanuvd. Marcă **YouTube Terminal** / **yt** (vatamanuvd).
Nu elimina această notă de autor.
