# Changelog

## Closed Beta v0.3.0 - 2026-08-20

- Added a visible Packages catalog with install/remove testing for the bundled
  CPU Boundary I/O and Waveform Compare packages.
- Added a split upper/lower waveform comparison window with independent
  navigation and optional marker/label alignment lock.
- Added CPU engineering JTAG logs that show successful and failed transaction
  stages, TX/RX/CHECK direction, bit counts, topology and observed IDCODEs.
- Added Settings-based update checks and SHA-256-verified EXE replacement.
- Kept input traces blank before observation and decoded BSDL `output3`
  high-impedance control as a dashed `Z` trace.
- Added bounded Case-scoped support submission/chat UI for configured support
  endpoints; no endpoint, token, BSDL or customer identifier is embedded.
- Bound the release archive to source commit `0f762447308f` and SHA-256
  `3007D165F6257D30FE86A31F690F187D4AA7BEADA1136AC5502E8D962BE96569`.
- Kept Rust source, Cargo manifests, private repository history, signing seeds,
  customer licenses, BSDL and waveform captures out of the public package.

## Closed Beta v0.2.8 - 2026-08-07

- Added Device ID copy and signed, device-bound `.cjlicense` import.
- Added waveform All/None selection, drag-to-zoom, and software edge trigger controls.
- Stabilized Pin List scrolling to reduce intermittent red table-border flicker.
- Bound the release archive to source commit `14110f77ebc1` and SHA-256
  `D45521B8C0A7363F63B74D7EC977AE177744B2A5CDEFEE85674E325B6707A8CB`.
- Kept signing secrets, customer licenses, source code, and private issuer tools out of the public package.

## Public preview v0.2.5 - 2026-07-28

- Published one canonical GitHub Releases download path for all evaluators.
- Bound the public archive to source commit `cb7bc9e7bb16` and SHA-256
  `FF5439E87F9B038229873863D6ED1BF3C7B18771178A0E50BFBA333D421EDFFB`.
- Documented the unsigned preview status and Windows warning behavior.
- Kept source code, private hardware data, and paid CLI/Tcl extensions out of
  the public repository.

## Documentation v0.2.5 - 2026-07-28

- Added public Trial overview and UI-first operating SOP.
- Documented FTDI, Intel/Altera, and AMD/Xilinx backend support boundaries.
- Documented BSDL/physical IDCODE validation.
- Documented waveform Time/Div, cursors, scan history, `.cjwave`, and long-capture policy.
- Added troubleshooting, privacy, download verification, and public feedback guidance.
- Explicitly separated implemented software support from pending physical hardware acceptance.
