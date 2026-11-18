# VIC1 interactive timber viewer (OBJ + interactive RTI + CT)

A static site built with Three.js. It loads an OBJ from public Cloudflare R2, displays selectable hotspots, and includes an embedded interactive RTI viewer (no RTI animation/video).

## Configure

Open `config.js` and paste:
- `objUrl`: public OBJ URL, preferably the ~67 MiB simplified model. Cloudflare R2 CORS must permit your website origin.
- `rtiViewerUrl`: **a complete publicly hosted OpenLIME viewer webpage URL**, not a raw `.rti` or `.ptm` file (optional).
- `ctViewerUrl`: already points to your vtk.js VIC1 CT viewer.


## Deploy

1. Create a separate GitHub repository, for example `vic1-obj-rti-viewer`.
2. Upload `index.html`, `config.js`, and `README.md` to the repository root.
3. Import it into Vercel. Framework: **Other**, no build command; root directory is the repository root.
4. Test with the public Vercel URL in a private/incognito window.
5. The large OBJ can take time to download and parse. Using OBJ directly is possible but less efficient than a compressed glTF/GLB.

## Create and publish hotspots

Click **Curator tools**, then **Place hotspot: ON**. Click the timber, type a title and note, choose the media, click Save hotspot. Click **Copy hotspot JSON** and paste the returned array into `hotspots: []` in `config.js`. Commit, redeploy. Browser-only edits are not published to other people.

Hotspot coordinates are normalized to the automatically scaled and centered model; editing the geometry or changing the OBJ version may require repositioning hotspots. OBJ has no physical voxel intensities and cannot replace the separate CT viewer.

## Safety and caveats

- Only publicly share the images/models with permission from rights holders.
- `rtiViewerUrl` must be a webpage. This template does not itself process native `.rti`/`.ptm` datasets.
- RTI iframe may be refused by the RTI host's frame protection; in that case use an external link or host the viewer on your own site.
- Large OBJ/MTL collections: this starter loads geometry with a default material. It does not load external MTL textures.
- The browser may need significant RAM to parse a 67 MB text OBJ file.

## This repaired version

- Fixes the scaling/centering transform in the original template, which could place valid models outside the camera view.
- Reports the number of meshes, triangles, and finite vertices when the model is loaded.
- Does not claim to repair an OBJ whose geometry is missing or whose vertex coordinates are invalid.
- Open browser Developer Tools > Console and look for `VIC1 OBJ geometry diagnostics` if loading still fails.
- Keep hotspots only after you verify the corrected model orientation: existing marker coordinates may need re-positioning.

## RTI mode
Only the interactive RTI iframe is present. RTI animation, MP4 player, and video-related configuration have been removed.
