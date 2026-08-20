# ChipJTAG Pro Trial

[繁體中文](README.md) | [English](README.en.md)

> See the hardware before it boots.

ChipJTAG Pro is a native Windows application for read-only JTAG hardware
observation and validation. It turns raw scan-chain data into waveforms and
structured hardware evidence that can be inspected, saved, reloaded, and
compared.

This public repository contains the trial download, operating guidance,
release notes, known limitations, and the public issue tracker. It does not
contain ChipJTAG Pro source code and is not an open-source software release.

## Current Release

- Version: `v0.3.0`
- Platform: Windows 10/11 x64
- UI: Native Rust `eframe/egui` with OpenGL
- Trial: Seven-day Pro evaluation from the first successful launch
- Release type: Closed Beta
- Advanced Automation / CLI / Tcl extension: Not included
- Authenticode: Not signed

## Download

Download only from the official
[ChipJTAG Pro Closed Beta v0.3.0 Release](https://github.com/blackjose007-stack/ChipJTAG-Pro-Trial/releases/tag/trial-v0.3.0).
Do not use old packages forwarded through chat, email, or third-party file
sharing services.

Files:

- `ChipJTAG-Pro-native-v0.3.0-seven-day-trial.7z`
- `ChipJTAG-Pro-native-v0.3.0-seven-day-trial.7z.sha256`
- `ChipJTAG-Pro-v0.3.0-x86_64.exe`
- `ChipJTAG-Pro-v0.3.0-x86_64.exe.sha256`

Archive size: `4,825,253` bytes

SHA-256:

```text
3007D165F6257D30FE86A31F690F187D4AA7BEADA1136AC5502E8D962BE96569
```

Verify the downloaded archive in PowerShell:

```powershell
Get-FileHash .\ChipJTAG-Pro-native-v0.3.0-seven-day-trial.7z -Algorithm SHA256
```

Do not extract or run the package if any character in the hash is different.
This preview is not Authenticode-signed, so Windows may display Unknown
publisher or a SmartScreen warning. SHA-256 confirms that the file matches the
published artifact; it does not authenticate the publisher.

## What ChipJTAG Pro Does

- Discovers supported JTAG adapters and scans a JTAG chain.
- Reads physical device IDCODE values.
- Imports BSDL and blocks scanning when the physical IDCODE does not match.
- Imports LPF/XDC pin assignments and I/O direction metadata.
- Observes approved boundary-scan states through a read-only `SAMPLE` path.
- Displays input, output, bidirectional, and high-impedance digital waveforms.
- Provides Time/Div, fixed T0, horizontal navigation, cursors, and scan history.
- Saves and reloads `.cjwave` recordings.
- Exports trial-limited Snapshot, CSV, VCD, Evidence, and Diagnostics files.
- Includes a native serial terminal, a supported Tera Term macro subset, and
  terminal log recording.
- Includes a visible Packages catalog with locally installable/removable CPU
  Boundary I/O and Waveform Compare Closed Beta packages.
- Shows bounded CPU engineering JTAG TX/RX/CHECK stages, bit counts, IDCODEs,
  and both successful and failed outcomes in the local log.
- Keeps software updates in Settings and verifies the downloaded EXE SHA-256.

## What It Does Not Do

- It does not program `.jed`, `.sof`, `.bit`, or other device images.
- It does not perform CPU debug or expose arbitrary JTAG commands.
- It does not execute `EXTEST`, `CLAMP`, or `HIGHZ`.
- It does not intentionally drive target outputs.
- It does not guarantee compatibility with every device, board, or chain.
- It does not include the paid Advanced Automation CLI/Tcl extension.

## Before Testing

1. Use Windows 10 or Windows 11 x64.
2. Prepare a non-production test board and the correct BSDL.
3. Install the required adapter driver and vendor tool.
4. Extract the archive to a local folder such as
   `C:\ChipJTAG-Pro-Trial`; do not run it from OneDrive or inside the archive.
5. Verify the SHA-256 before launching `ChipJTAG-Pro.exe`.

Adapter prerequisites:

| Adapter | Required software |
| --- | --- |
| FTDI MPSSE | FTDI D2XX driver |
| Intel/Altera USB-Blaster | Quartus Programmer or Quartus Lite with `quartus_stp.exe` |
| AMD/Xilinx Platform Cable or Digilent JTAG | Vivado or Vivado Lab Edition with `vivado.bat`/`vivado_lab.bat` and `hw_server` |

All three backends remain Preview until a public known-good
cable/driver/tool/target/BSDL matrix is completed.

## Pilot Validation

The current pilot validates existing features only:

1. Native application launch and trial status.
2. Adapter discovery and connection.
3. BSDL import and physical IDCODE matching.
4. Start/stop scan and Interface Log diagnostics.
5. Real waveform transitions and navigation.
6. Scan history behavior.
7. `.cjwave` save/load timestamp and transition fidelity.
8. Export behavior under trial limits.

Use the [three-person pilot checklist](docs/PILOT_VALIDATION.md) to record the
same environment and evidence for each tester.

## Known Validation Boundaries

- AMD/Xilinx physical cable and target acceptance is incomplete.
- General stable `<= 1 ms` physical capture is not yet claimed.
- Long-duration recording still requires physical endurance testing.
- Multi-device AMD/Xilinx waveform capture is outside the v0.3.0 acceptance
  scope.
- CPU Boundary I/O remains an engineering preview with zero officially
  supported CPU models. Local BSDL load or capture is not a model-support claim.
- The bundled package catalog does not download payloads from the network.

## Feedback and Data Safety

Use [GitHub Issues](https://github.com/blackjose007-stack/ChipJTAG-Pro-Trial/issues)
for general, sanitized feedback.

Do not upload customer BSDL, LPF, XDC, QSF, netlists, schematics, private
waveforms, diagnostics, terminal logs, device identifiers, cable serial
numbers, account details, or other confidential hardware data to a public
Issue.

Include the following non-confidential information when reporting a problem:

- ChipJTAG Pro version and archive SHA-256
- Windows version
- Adapter type
- Vendor tool and version
- Target FPGA/CPLD family
- Expected result and actual result
- Reproduction steps
- Sanitized Interface Log excerpt

## License

The trial is provided for evaluation under the
[ChipJTAG Pro Evaluation License](LICENSE.md). It is provided as-is and must
not be the sole basis for production, destructive, or safety-critical hardware
decisions.
