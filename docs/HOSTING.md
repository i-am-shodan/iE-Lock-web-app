# Hosting the Web Console

This guide covers the prebuilt static site. It does not require Node.js, a
database, a vendor account, or a server-side build.

## Choose a Trusted Origin

- Use HTTPS with a certificate trusted by the device. Plain HTTP on a LAN IP
  address and opening an HTML file directly are not suitable for lock access.
- Use a dedicated origin where possible. Different paths on the same origin do
  not isolate browser storage from one another.
- Treat control of the hosting account and published JavaScript as control of
  a credential-handling application. Do not co-host untrusted applications.
- An HTTPS page still needs a compatible browser: use Bluefy on iPhone, or a
  Web Bluetooth-capable browser such as Chrome or Edge on Windows.
- Self-hosting does not strengthen the lock's Bluetooth protocol.

See [PIN storage and privacy](../README.md#pin-storage-and-privacy) before
deciding where to host the site.

## GitHub Pages: Publish from a Branch

These steps apply to a GitHub repository where Pages is available and you have
permission to configure it.

1. Make sure the intended publishing branch contains the complete site,
   including `index.html`, `assets/`, `favicon.svg`, `icons.svg`, and `.nojekyll`.
   Local files that have not been committed and pushed will not be published.
2. In the repository's **Settings > Pages**, choose **Deploy from a branch**.
3. Select that branch and **/ (root)**, then save. Do not select `/docs`: that
   directory holds documentation, not the site entry point.
4. Wait for GitHub's deployment to finish. Use the exact HTTPS URL shown by
   Pages rather than guessing the repository URL.
5. Open that URL and follow the verification checklist below.

The existing relative asset URLs allow the site to be served under a repository
path. No GitHub Actions build workflow is required for branch-based publishing.
Pages publishes files, not a private lock service: do not put credentials,
captures, or private documents anywhere in the publishing tree.

For service-specific setup and domain configuration, consult the
[GitHub Pages documentation](https://docs.github.com/en/pages).

## Other Static Hosts

Publish the static entry point, icons, and the entire `assets/` directory,
preserving their relative paths. Configure the host to:

- Serve the site over trusted HTTPS.
- Serve JavaScript and CSS with appropriate content types.
- Return the actual asset files, not an HTML fallback for missing assets.
- Avoid keeping an old entry page paired with new bundles, or vice versa.

The repository documentation is not required for the application to run. The
site does not need a reverse-proxied API or Bluetooth access on the web server;
Bluetooth communication happens on the user's device.

## Local Preview on Windows

For a visual preview, if Python 3 is installed, open PowerShell in the repository
root and run:

```powershell
python -m http.server 8000 --bind 127.0.0.1
```

Open `http://localhost:8000` on that same Windows machine. Stop the server with
**Ctrl+C**. This command binds only to the loopback interface; it is not a
production hosting setup.

Compatible desktop browsers generally treat localhost as a secure context, but
Bluetooth support and permissions are still required. On an iPhone, `localhost`
means the phone itself, not your PC. Use the trusted HTTPS deployment for Bluefy
testing; changing the URL to your PC's ordinary HTTP LAN address is not a
substitute.

## Verification Checklist

### Without a Lock

- [ ] The published URL loads over HTTPS without certificate warnings.
- [ ] JavaScript, CSS, icons, and fonts load without missing-file or MIME errors.
- [ ] The console renders correctly at desktop and phone widths.
- [ ] Browser developer tools show no failed application asset requests.
- [ ] The README links to the correct setup, troubleshooting, and safety guidance.

A rendered page verifies hosting only, not Bluetooth or lock compatibility.

### Optional Authorized Hardware Check

- [ ] Use only a lock you own or are authorized to manage.
- [ ] Keep the door physically accessible and an independent means of entry.
- [ ] Use the supported browser, connect, and authenticate with known credentials.
- [ ] Check read-only status and battery information first.
- [ ] If testing unlock, issue it explicitly and confirm the physical result.
- [ ] On timeout, inspect the lock before retrying.

Do not enroll or delete credentials, restrict access, change the administrator
PIN, or factory-reset a lock merely to check a deployment.

## Updating and Rolling Back

1. Record the current deployed commit or release so it can be restored.
2. Obtain a trusted, complete built release. This checkout cannot rebuild the
   application from original source.
3. Publish its matching entry page and assets together. Preserve repository
   documentation and applicable license notices.
4. Run the hosting checks above. Reload the page on an existing browser session
   as well as a fresh one to catch stale asset references.
5. If verification fails, redeploy the previous complete release; do not mix
   files from different builds.

Changing the scheme, hostname, or port changes the browser origin and may require
selecting the lock and saving its PIN again. Clearing all site data also removes
saved local credentials. A website rollback does not undo commands already
accepted by a physical lock or restore its deleted credentials.
