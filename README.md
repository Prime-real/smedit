# Prime Edits — UI starter

This is a polished UI prototype based on the supplied core structure:
Web App → Prime Edits → Client Upload / Final Edits.

## Included UX
- Client / Final workspace split
- Drag & drop media upload UI
- Image/video thumbnails
- Search
- Favorites
- Smart Asset Scan placeholder
- Delete Manager placeholder
- Separate Client / Editor / Delete access gates
- Responsive dark creator-dashboard design

## Important security note
The HTML intentionally does NOT contain the real passwords. A password placed in frontend JavaScript can be inspected by anyone who downloads the page.

For the production version:
1. Deploy the UI to Vercel.
2. Put access secrets in Vercel Environment Variables.
3. Use Vercel API routes/serverless functions to validate access.
4. Use signed upload/download URLs so storage credentials never reach the browser.
5. Keep the delete password server-side and log every delete.

## Recommended storage architecture

Vercel = UI + API routes
Cloudflare R2 = actual video/image/object storage
Supabase Postgres = small metadata database (filename, side, favorite, object key, timestamps)

This is better for a video workflow than storing large videos inside a frontend/Vercel deployment.

## Smart features for v2
- Duplicate detection using SHA-256 hash
- Automatic image/video detection
- Video duration + resolution + FPS extraction
- Favorites
- Tags: raw / selected / final / thumbnail
- Upload progress + resumable uploads
- Final delivery status
- Preview player
- Search by filename/tag/type
- Expiring signed links
- Delete confirmation + server-side delete PIN
- Activity log

## Storage note
Do not rely on the Vercel filesystem as permanent media storage. Use object storage.

Cloudflare R2 currently includes 10 GB-month of Standard storage, 1 million Class A operations and 10 million Class B operations per month, with no egress charge. Its object size limit is much larger than typical creator videos. Always re-check the provider's current pricing before relying on a free allowance.

Supabase Free is useful for metadata/auth, but its current Free Storage allowance is 1 GB and the Free max file upload size is 50 MB, so it is not a good primary store for large raw videos.
