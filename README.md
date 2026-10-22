# vpc-visual — Ravi's Cloud Society

An animated, beginner-friendly diagram that explains an AWS Virtual Private Cloud (VPC) through the story of Ravi, a shop owner with a gated housing society. The map grows one step at a time, with moving packet icons following network paths. Built with plain HTML, CSS and JavaScript; no build step, framework or runtime dependencies.

> **Learning illustration:** this is a teaching aid, not a production AWS architecture or deployment template. The diagram uses simplified routes and security rules.

## What it is

- Nine clickable steps, with earlier parts staying visible as the network grows.
- SVG network diagram with animated dashed routes and moving packet icons.
- Auto-play advances every five seconds; Reset returns to step one.
- Light/dark page theme, responsive layout and reduced-motion support.
- Plain-language explanations beside the technical terms.

## Moving objects

| Object | Story meaning | What it represents |
| --- | --- | --- |
| ✉️ Envelope | A visitor arrives at Ravi's gate | Incoming visitor/web request |
| 💾 Floppy disk | Work records move between workers and storage | Data moving between web, app and database components |
| 🔁 Repeat arrows | The records room keeps a live copy | Database replication between zones |
| 📦 Package | A resident fetches a software update | Outbound internet traffic through a NAT Gateway |
| 😈 Devil | An intruder tries to enter a private area | Unwanted traffic stopped by a security boundary in this illustration |
| 🔒 Lock | Ravi's office uses a secret tunnel | VPN connection from an office network to a VPC |
| 🤝 Handshake | A trusted partner gets a private road | VPC Peering connection |

## The 9 steps

1. **The fenced plot — VPC:** An AWS Cloud Region and Ravi's isolated VPC (`10.0.0.0/16`).
2. **Two buildings — Availability Zones:** Two separate zones to help improve resilience.
3. **Public and private homes — Subnets:** Gold public subnets and purple private subnets in both zones.
4. **The main gate — Internet Gateway and routes:** The Internet, visitors, a route-table label and a moving envelope.
5. **Reception — Load Balancer:** Requests are shared between web servers in both zones.
6. **App and data:** App servers, a primary database and a live-copy database with a replication path.
7. **Delivery counter — NAT Gateway:** A private resource's software update goes out through NAT and the internet gate.
8. **Security:** Security Group (SG) door-guard tags, subnet NACL gate-guard tags, and an intruder that is blocked.
9. **Private links:** An office VPN tunnel to the private subnet and a peering link to a Partner VPC.

## Run locally

You only need Python 3 (or any static file server).

1. Download and unzip the project.
2. Open a terminal and change into the project folder:

   ```bash
   cd vpc-visual
   ```

3. Start the local server:

   ```bash
   python3 -m http.server 8000
   ```

4. Open <http://localhost:8000> in your browser. Press `Ctrl+C` in the terminal to stop the server.

You can open `index.html` directly, too, but a local server is the recommended way to test it.

## Host on GitHub Pages

1. Create a new GitHub repository named **`vpc-visual`**, then unzip this folder and upload its contents (keep `index.html` at the repository root); commit to the `main` branch.
2. In the repository, open **Settings → Pages**. Under **Build and deployment**, choose **Deploy from a branch**, select **main** and **/ (root)**, then click **Save**.
3. Wait for the Pages deployment to finish. Your site URL will appear in **Settings → Pages** (usually `https://YOUR-USERNAME.github.io/vpc-visual/`).

## Project structure

```text
vpc-visual/
├── index.html       # Page structure and controls
├── css/
│   └── style.css    # Theme, responsive layout, motion and focus styles
├── js/
│   └── app.js       # Step data, SVG helpers, diagram and interactions
├── .nojekyll        # Tells GitHub Pages not to run Jekyll processing
├── LICENSE          # MIT license (replace YOUR NAME)
└── README.md        # This guide
```

## Customise the text

- Open `js/app.js` and edit the `steps` array. Each item contains `title`, `short`, `tag`, `plain`, `technical` and `watch` text.
- The step drawing is in `render()`. The `if (current >= N)` blocks add the components for step N. Keep `current` thresholds in order so clicking earlier steps hides later components.
- SVG positions use the fixed `viewBox="0 0 1100 620"`. Move a component by adjusting its `x`/`y` values and update any connecting path coordinates to match.

## Customise the colours and theme

- Page colours live in the CSS variables at the top of `css/style.css` under `:root`; dark page-theme overrides are under `body.dark`.
- Diagram colours are SVG fill/stroke values in `js/app.js`. Blue marks cloud/zones, teal marks the VPC, gold marks public networking, purple marks private networking, red marks security and green marks trusted office/partner links.
- The diagram intentionally remains a dark navy stage in both page themes so the colour key stays consistent.
- The Google Font Bricolage Grotesque is loaded from Google Fonts with system-font fallbacks. An internet connection is needed for the hosted font; the page itself still works offline with a fallback font.

## Accessibility notes

Buttons have visible keyboard-focus outlines, the current lesson is announced via an `aria-live` caption, and `prefers-reduced-motion` disables most motion. Packet movement uses SVG `<animateMotion>` and may vary slightly by browser.
