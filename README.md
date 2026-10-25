# Reachy Mini × Gemma 4 — a fully on-device robot companion

Project page for a Reachy Mini desk robot driven by Gemma 4 E4B running entirely on a
16 GB NVIDIA Jetson Orin NX. There is no cloud service in the loop, and it works offline.
Built by [Mihai Chiorean](https://github.com/mihai-chiorean) for the Gemma 4 hackathon.

Live page: https://mihai-chiorean.github.io/reachy-gemma4-edge/

The site is a single static `index.html` served by GitHub Pages from the root of the `main`
branch. There is no build step, no external JavaScript, and no analytics.

## Swapping in the demo video

Near the top of `index.html` there is one line:

```html
<script>const YOUTUBE_VIDEO_ID = "REPLACE_WITH_VIDEO_ID";</script>
```

Replace `REPLACE_WITH_VIDEO_ID` with the video's ID: the part after `watch?v=` in
`https://www.youtube.com/watch?v=VIDEO_ID`, or after `youtu.be/` in a short link. While the
placeholder is still there, the page shows a "Demo video coming soon" box instead of a player.
The player uses the `youtube-nocookie.com` embed.

Pick one of these ways to make the change:

**Local clone**

```sh
sed -i 's/REPLACE_WITH_VIDEO_ID/VIDEO_ID/' index.html
git commit -am "Add demo video" && git push
```

(On macOS use `sed -i '' ...`.)

**`gh` one-liner, no clone needed** (set `VID` to the video ID):

```sh
VID=VIDEO_ID; R=mihai-chiorean/reachy-gemma4-edge; gh api repos/$R/contents/index.html --jq .content | base64 -d | sed "s/REPLACE_WITH_VIDEO_ID/$VID/" > /tmp/index.html && gh api -X PUT repos/$R/contents/index.html -f message="Add demo video" -f content="$(base64 -w0 /tmp/index.html)" -f sha="$(gh api repos/$R/contents/index.html --jq .sha)"
```

**GitHub web editor**: open `index.html` on GitHub, click the pencil icon, change the one
line, and commit to `main`.

GitHub Pages redeploys automatically after each push to `main`; the change is usually live
in about a minute.

## License

The page content is released under the MIT License; see [LICENSE](LICENSE).
