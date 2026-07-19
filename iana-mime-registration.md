# IANA Media Type registration — application/vnd.capsium.package

Draft registration per RFC 6838 (vendor tree). Submit via
https://www.iana.org/form/media-types (a ~5-minute manual step; the form
mirrors the fields below).

- **Type name**: `application`
- **Subtype name**: `vnd.capsium.package`
- **Required parameters**: none
- **Optional parameters**: none
- **Encoding considerations**: binary. A Capsium package is a ZIP archive
  (ISO/IEC 21320-1) whose member files are UTF-8 JSON configuration files
  and arbitrary binary or text content.
- **Security considerations**:
  - Packages carry a `security.json` manifest of SHA-256 checksums covering
    every member file; conformant reactors MUST verify these and reject the
    package on any mismatch.
  - Packages MAY carry an RSA-SHA256 digital signature (`signature.sig`)
    and MAY be encrypted as a whole (AES-256-GCM with an RSA-OAEP-wrapped
    data-encryption key).
  - As with all ZIP formats, implementations MUST guard against archive
    path traversal (zip-slip) and decompression bombs; conformant
    implementations reject entries that escape the extraction root.
  - Packages may contain HTML/JS that executes in the serving context;
    sandboxing guidance is given in CC 62001.
- **Interoperability considerations**: the archive layout and the five
  configuration files (`metadata.json`, `manifest.json`, `routes.json`,
  `storage.json`, `security.json`) are specified by CC 62001, published at
  https://www.capsium.org/standard/ . Conformance classes (core and
  optional modules) are defined therein.
- **Published specification**: CC 62001, _Common architecture for portable
  secure information interchange and unified management (Capsium)_.
  https://www.capsium.org/standard/ (HTML) and
  https://www.capsium.org/standard/cc-62001.pdf (PDF).
- **Applications that use this media type**: capsium (Ruby packager and
  reactor, https://rubygems.org/gems/capsium), capsium-lua (nginx/OpenResty
  reactor), capsium-js (TypeScript runtime, service-worker reactor, Node
  reactor), capsium-webextension (browser extension).
- **Fragment identifier considerations**: none.
- **Additional information**:
  - Magic number(s): ZIP local file header signature `50 4B 03 04`
  - File extension(s): `.cap`
  - macOS UTI: `org.capsium.package`
- **Intended usage**: COMMON
- **Person & email address to contact for further information**:
  Ribose Inc., open.source@ribose.com — https://www.ribose.com
- **Author/Change controller**: Ribose Inc. (https://github.com/capsiums)
