# Security Policy

This client handles credentials and can operate a physical lock. Use it only
with locks you own or are authorized to manage, and keep an independent means
of entry. This policy is reporting guidance, not a security certification or a
guarantee of compatibility.

## Scope and Support

Reports about the web client, saved credentials, hosting guidance, and unsafe
command behavior are welcome. Include the affected commit or deployed release:
this repository does not currently declare a supported-version matrix, a
response-time commitment, or a guaranteed patch schedule.

The lock's firmware, vendor applications, browser, operating system, and hosting
provider are separate components. Report issues in those products to their
respective maintainers as appropriate. Findings in the historical Android
analysis do not by themselves establish a vulnerability in the web client.

## Report Privately

**Do not publish exploit details, credentials, or raw captures in a public
issue, discussion, or pull request.**

1. On GitHub, check the repository's **Security** tab for **Report a
   vulnerability**. If private vulnerability reporting is enabled, use it.
2. If that option is unavailable and no private contact has been published,
   open an issue asking only for a private security contact. Do not describe the
   vulnerability, identify an affected lock or person, or attach evidence there.
3. Wait for an agreed private channel before sharing sensitive details.

This checkout does not specify a verified private contact address. Do not send
reports to guessed email addresses or assume a public issue is private.

In the private report, provide:

- Affected commit or release, browser, operating system, and hosting context.
- A concise description of the impact and required preconditions.
- Minimal reproduction steps using your own authorized test environment.
- Expected and actual behavior, with sanitized evidence.
- Whether the behavior was observed on hardware, simulated, or inferred.
- Any known mitigation and whether the issue has already been disclosed.

Do not send real PINs, temporary codes, personal unlock histories, credential
lists, Bluetooth identifiers, or browser storage exports. Use synthetic values
and explain any redactions. Coordinate disclosure before publishing details
that could expose an installed lock.

## If You Suspect Exposure

- Stop using a deployment you do not trust; protect physical access first.
- Use a trusted, authorized management method to change exposed credentials or
  revoke access as appropriate for the lock.
- **Forget saved PIN** removes a local entry; it does not change the lock's PIN
  or revoke access on other devices.
- A site rollback, browser disconnect, or cleared cache cannot undo an unlock
  or a credential change already accepted by the lock.
- If you operate the host, secure the hosting account and investigate the
  published files before resuming use.

For the browser-storage trust model and its limitations, see
[PIN storage and privacy](README.md#pin-storage-and-privacy).
